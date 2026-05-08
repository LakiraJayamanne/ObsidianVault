---
tags:
  - persona
  - voice-assistant
  - in-progress
date: 2026-04-04
---

# Persona — Build Notes

## Stack
| Component | Choice |
|---|---|
| Wake word + snaps | OpenWakeWord (fully local, no account) |
| STT | Whisper (local) |
| Brain | Ollama — llama3.1 8B |
| TTS | edge-tts — en-GB-RyanNeural |
| Text input | Terminal + WhatsApp (planned) |

## Project Location
`/home/lakira/Documents/Projects/MyPersona/`

## File Structure
```
MyPersona/
├── main.py        # entry point
├── wake.py        # OpenWakeWord (voice wake word + two snaps)
├── stt.py         # Whisper STT
├── brain.py       # Ollama
├── tts.py         # edge-tts
├── input.py       # terminal/WhatsApp text input
└── config.py      # settings
```

## config.py — Done ✓
```python
wake_word = "Persona"
voice = "en-GB-RyanNeural"
brain_model = "llama3.1"
input_device = None
timeout = 5
personality = "Your name is Persona (inspired by the games, YOU are my persona)." \
"You are an assistant for me, Kira. pronounced Kee-Ruh. You are intelligent calm" \
"and friendly - like EDITH from Spider-Man, or JARVIS/FRIDAY from Iron-Man. You speak concisely" \
"since your responses are read aloud. You're not overly formal, but profesional when needed." \
"You can help with anything. Questions, tasks, advice or just a chat. Address Kira by name occasionally." \
"Sir works too. Heck even sometimes, Spidey works too. keep the chances of that low though. Never break character. You are my persona."
```

## tts.py — Done ✓
```python
import edge_tts
import subprocess
import asyncio
import tempfile
import config

async def speak(text):
    text = text.replace("Kira", "Keera")
    communicator = edge_tts.Communicate(text, config.voice)
    tmp_file = tempfile.mktemp(suffix=".mp3")
    await communicator.save(tmp_file)
    subprocess.run(["mpv", tmp_file], stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL)

if __name__ == "__main__":
    asyncio.run(speak("Hello Kira, I am JARVIS. All systems are online."))
```

## brain.py — In Progress
- Imports: `ollama`, `config`
- Function: `def think(text):`
- Needs to call `ollama.chat()` with:
  - model: `config.brain_model`
  - messages: system (personality) + user (text)
- Next step: write the ollama.chat() call

## Wake Word Notes
- Two snaps (not one) to avoid accidental triggers
- Both "Persona" wake word AND two snaps run simultaneously
- Whichever triggers first activates the assistant

## TTS — Pronunciation Fix
- "Kira" replace → "Keera" before passing to edge-tts

## STT Optimization Plan (researched 08/05/2026)

**Problem:** Whisper tiny on CPU = ~24s. Kills the pipeline.

**Fix — in order:**
1. **Build whisper.cpp with ROCm/HIP on Fedora**
   - Target: `gfx1031` (RX 6700)
   - Use `base` model (better accuracy than tiny, still fast on GPU)
   - Expected: 2-4s (down from 24s)
   - Fedora gotcha: LLVM is at `/usr/lib64/llvm18/bin` not `/opt/rocm/bin` — expect build pain
   - Guides: AMD ROCm blog "Speech-to-Text on AMD GPU", davidguttman/whisper-rocm on GitHub
2. **Swap edge-tts → Piper TTS**
   - edge-tts phones home to Microsoft servers (network latency)
   - Piper is fully local, sub-1s on CPU, drop-in replacement
3. **Add VAD (voice activity detection)**
   - Start transcription the moment speech ends instead of fixed silence window
   - Silero VAD is fine on CPU for this
4. **Stream TTS tokens** as LLM generates (don't wait for full response)

**Don't use faster-whisper** — CUDA-only, no AMD support.
**LLM is already fine** — llama3.2:3b at 0.5s on GPU, leave it.

**Target after fixes:** ~3-5s full pipeline (wake → spoken response)

---

## Planned Features
- Voice input (wake word → speak)
- Text input via terminal
- WhatsApp input
- Voice always speaks back (edge-tts)
- Persistent memory / Obsidian vault RAG (v2)
- Assistant name: JARVIS (placeholder until Persona game character chosen)
