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

**Updated findings (deep research 08/05/2026):**
- The 24s STT is likely a code issue, not a GPU issue. Check:
  - Using `openai-whisper` instead of `faster-whisper` (4-10x slower)
  - Model reloading on every call instead of once at startup
  - No VAD — recording 15-20s of silence before sending
- **Moonshine STT** (`pip install moonshine-voice`) — ~270ms on CPU, beats Whisper Large V3 accuracy. Try this first.
- **whisper.cpp with Vulkan** (`-DGGML_VULKAN=1`) — easier than ROCm HIP on Fedora, ~0.2s on GPU. ROCm HIP PR doesn't cover gfx1030 (RX 6700) — use Vulkan instead.
- **Silero VAD** — stops recording the moment speech ends instead of waiting for silence timeout
- **Streaming LLM → TTS** — buffer into sentences, start TTS on first sentence while LLM still generating the rest. Biggest single architecture win.
- **Piper TTS** (`en_GB-alan-medium` voice) — fully local, streaming synthesis, sub-1s on CPU
- **Qwen3:1.7b** — may outperform llama3.2:3b for voice. Use `/no_think` mode + `num_predict 150`
- **Custom "Persona" wake word** — CoreWorxLab/openwakeword-training, 20-50 voice samples + 4-8hr training

**Don't bother with:** faster-whisper (CUDA-only officially), ROCm HIP whisper.cpp on gfx1030, Bark TTS, StyleTTS2, openai-whisper library

**Target after fixes:** ~1.5s to first spoken word (Moonshine + streaming LLM→TTS)

**Top repos to reference:**
- sancliffe/ollama-STT-TTS — nearly identical stack, clean code
- KoljaB/RealtimeVoiceChat — gold standard pipeline, sentence streaming pattern
- isair/jarvis — dual model + tool routing
- eauchs/speech-to-speech-pipeline — barge-in/interrupt implementation
- beecave-homelab/insanely-fast-whisper-rocm — full ROCm GPU STT if needed later

---

## Acknowledgement Pattern (UX idea — 08/05/2026)

For long tasks (deep research, file ops, etc.) — don't make the user wait in silence.
JARVIS should immediately speak a short acknowledgement, THEN do the work:

> "On it sir, researching xyz — I'll report back when it's done."

**How it works:**
1. STT captures the query
2. LLM does a fast intent classification (is this a quick answer or a long task?)
3. If long task → speak acknowledgement immediately → run task in background → speak result when done
4. If quick answer → respond normally

This makes latency feel near-zero regardless of actual task duration.

---

## Planned Features
- Voice input (wake word → speak)
- Text input via terminal
- WhatsApp input
- Voice always speaks back (edge-tts)
- Persistent memory / Obsidian vault RAG (v2)
- Assistant name: JARVIS (placeholder until Persona game character chosen)
