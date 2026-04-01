---
tags:
  - jarvis
  - voice-assistant
  - python
updated: 2026-04-01
---

# Voice Assistant Project

> JARVIS-style ambient voice assistant. Speak to it while coding or doing everyday tasks. It listens, processes, and responds naturally.

---

## Stack (Decided 01/04/2026)

| Component | Choice | Notes |
|---|---|---|
| Wake word | Porcupine (Picovoice) | Free tier, accurate, low CPU. Wake word: "Persona". |
| STT | Whisper (local) | Runs on-device, no API |
| Brain | claw-code | https://github.com/instructkr/claw-code |
| TTS | edge-tts | Free, cross-platform, good voice quality |

---

## Status

- [ ] Desktop dual boot (Fedora + Hyprland) — prerequisite
- [ ] claw-code — get set up
- [ ] Desktop rice (Quickshell) — after dual boot
- [ ] Voice assistant — build starts after above

**Not started yet. Waiting on desktop setup.**

---

## Architecture

```
[Wake word] → [Record speech] → [Whisper STT] → [claw-code brain] → [edge-tts] → [Play audio]
     ↑                                                                                    |
     └────────────────────────────── loop ──────────────────────────────────────────────┘
```

---

## Decisions

- **Wake word vs hotkey**: Wake word chosen. More natural, proper JARVIS feel.
- **Local STT**: Whisper runs locally — no cloud, no latency, privacy intact.
- **Brain**: claw-code (Rust-based AI agent harness with tool use, plugins, MCP support).
- **TTS**: edge-tts over ElevenLabs — free, no API limits, cross-platform, good enough quality.
- **Platform**: Both Windows and Linux. Build with cross-platform in mind.
- **Name**: Persona. Ties into Persona Quickshell rice. Wake word: "Persona".

---

## Notes

- RX 6700XT on desktop will handle Whisper well — don't build/test on laptop (iGPU)
- claw-code is Rust-based, worth reading the repo before building around it
- edge-tts calls Microsoft's servers under the hood — not truly offline, but no account/key needed
