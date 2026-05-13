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

---

## Deep Research: Architecture Ideas (13/05/2026)

### Barge-in / Interrupt Mid-Speech
- **Vocalis** (github.com/Lex-au/Vocalis) — gold standard for this. Speech-to-speech with mid-speech interruption, chunked TTS streaming, silence detector + interrupt detector running in parallel. Clean Python, worth reading the architecture.
- Pattern: frontend audio buffer → silence detector → interrupt detector → backend interrupt handler
- Current Persona gap: no way to stop JARVIS mid-response

### Presence Detection (no wake word needed)
- Webcam + OpenCV — detect when you sit down at your desk, greet automatically. Know when you've walked away.
- No need to say wake word every time. JARVIS just knows you're there.
- Project reference: vannu07/jarvis (face recognition + hotword detection combo)

### Emotion Detection
- BERT model reads voice tone — frustrated → responds differently than curious/happy
- Makes the interaction feel natural rather than robotic
- v3/v4 feature, not urgent

### MCP Integrations
- Home Assistant has an official MCP server — when Pi-hole/smart home is set up, JARVIS controls it natively
- No custom tool code needed for: GitHub, Notion, Slack, databases — all plug straight in via MCP
- isair/jarvis uses embedding-based tool selection — picks relevant tools per query instead of passing everything to the LLM each time. Keeps context clean and fast.

### Proactive JARVIS (biggest idea)
- Instead of only responding when called, JARVIS watches for triggers and speaks up unprompted
- Examples: "You have a lecture in 10 minutes", "Your build finished", "Weather's changed", "It's been 2 hours since you last drank water"
- This is what separates a voice chatbot from a real assistant
- Implementation: background daemon with scheduled checks + event listeners → speaks when condition met

### Intent Classification
- Tiny separate model just to classify intent before the main brain handles it
- isair/jarvis uses gemma4:e2b for this
- Prevents false triggers, routes to right tool faster, stops the main LLM wasting context on "did you mean to talk to me?"

### Dictation Mode
- Hold a hotkey → speak → transcription pasted into any app
- Free offline alternative to WisprFlow / Whisper Flow
- Useful outside of assistant interactions — notes, messages, code comments

---

## Research: vierisid/jarvis (13/05/2026)

Studied the open-source [usejarvis.dev](https://usejarvis.dev) project for architecture ideas. Fully open source, supports Ollama (free), Docker-based.

**Ideas worth stealing:**

1. **Sidecar architecture** — a lightweight Go binary runs on the machine and gives the brain "hands": desktop automation, Win32 API on Windows, X11 on Linux. This is the biggest gap in the current Persona stack — no desktop control at all.

2. **Authority engine** — gates actions and keeps audit logs before executing anything. Good for safety when tools can open apps, run commands, etc.

3. **Multi-agent** — specialist LLMs for different task types rather than one brain doing everything. e.g. a fast model for quick answers, a smarter model for complex tasks.

4. **Screen awareness** — the daemon can see what's on screen and act on it. Combined with sidecar desktop control, this is what makes it feel like a real JARVIS.

5. **Visual workflow builder** — React UI with 50+ node types for building automations. Overkill for now but interesting longer term.

**Stack:** Bun + TypeScript (daemon), Go (sidecar), React 19 + Tailwind (UI), SQLite (memory/logs), openwakeword (same as Persona).

**Repo:** https://github.com/vierisid/jarvis

---

## Feature Priority Order (13/05/2026)

1. **STT latency (Moonshine)** — nothing else matters if the pipeline feels slow. Do on Fedora first.
2. **Barge-in / interrupt** — makes it feel like a real conversation. Vocalis has the pattern.
3. **Proactive JARVIS** — background daemon watching for triggers, speaks unprompted. Makes it feel alive.
4. **Presence detection** — DroidCam on Samsung M21 → OpenCV face detection. No webcam needed.
5. **Intent classification** — tiny model to prevent false triggers (gemma4:e2b pattern from isair/jarvis).
6. **MCP integrations** — once pipeline is solid. Home Assistant, GitHub etc.
7. **Dictation mode** — hold hotkey → speak → paste into any app. Offline WisprFlow alternative.
8. **Apple Watch integration** — Watch → iPhone Shortcut → HTTP POST → Persona Flask/FastAPI endpoint. Also works in reverse: Persona pushes notifications → appear on watch. ~10 lines to add the API.
9. **Emotion detection** — v3/v4, not urgent.

---

## Reference: openclaw.ai (noted 02/04/2026, confirmed 13/05/2026)

- Persistent local AI assistant by Peter Steinberger
- Controlled via WhatsApp/Telegram/Discord/Signal/iMessage
- Browser control, file read/write, command execution, 50+ integrations
- Supports Claude, GPT, local models
- Free and open source
- Ismail (Lakira's friend) uses this for his own JARVIS setup
- Different approach to Persona — messaging-app controlled vs voice-first
