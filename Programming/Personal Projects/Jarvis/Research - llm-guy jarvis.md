---
tags:
  - spid
  - research
  - voice-assistant
links:
  - "[[Homelab & JARVIS Architecture]]"
  - "[[Persona Build Notes]]"
source: https://github.com/llm-guy/jarvis
reviewed: 2026-05-15
---

# Research — llm-guy/jarvis

314 stars. Local, privacy-first voice assistant. Clean minimal codebase (basically main.py + tools/).

---

## What it does

Wake word → conversation mode (30s timeout) → LangChain agent → LLM tool-calling → TTS response. Fully offline capable.

---

## Worth stealing

### 1. Conversation timeout (30s)
After wake word triggers, stays in conversation mode for 30 seconds of inactivity then drops back to wake-word listening.
- SPID doesn't have this yet
- Prevents sessions staying open forever
- Simple: track `last_speech` timestamp, exit conversation loop if `time.time() - last_speech > 30`

### 2. ARP scan tool
Scans local network to see which devices are online.
- Useful for presence detection: "is dad's phone on the network?" = is dad home
- Pairs well with SPID on Pi 5 (always on, always on the network)
- Uses `subprocess` + `arp -a` or `python-nmap`

### 3. Screenshot + OCR (pytesseract)
Captures screen and extracts text instantly — no LLM needed.
- Faster and free vs describe_screen with gemma3:4b
- Best used as a first pass: pytesseract for text-heavy screens, gemma3 for visual/layout understanding
- `pytesseract.image_to_string(PIL.ImageGrab.grab())`

### 4. LangChain tool-calling pattern
Cleaner agent loop than raw Ollama tool-calling. Handles multi-step tool chains better.
- Worth considering when SPID's tool set grows larger (10+ tools)
- Not worth switching to now — current setup is leaner
- Revisit when tool complexity increases

---

## Not worth copying

- **SpeechRecognition (Google STT)** — worse than faster-whisper in every way
- **pyttsx3 TTS** — robotic, no personality. Kokoro is miles ahead
- **qwen3:1.7b** — already using 8b
- **LangChain as a dependency now** — too heavy for current SPID stack

---

## Priority

| Feature | Priority | Notes |
|---|---|---|
| Conversation timeout | High | Quick to add, clean UX |
| ARP scan tool | Medium | Presence detection use case |
| pytesseract OCR | Medium | Fast screen reading, complement to gemma3 |
| LangChain migration | Low | Revisit when tool count grows |
