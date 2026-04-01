---
tags:
  - jarvis
  - archive
date: 2025-08-24
---

# Old Project Notes — August 2025

> Archived from original JARVIS project. Kept for reference — some concepts still valid.

---

## The Core Loop

Every voice assistant follows the same pattern:

```
1. Listen for wake word
2. Record Speech
3. Speech To Text (STT)
4. Process with AI
5. TTS
6. Play Audio
7. Loop back to step 1
```

The loop is simple. The complexity is in HOW you implement each step:
- Step 1: How to detect wake word efficiently?
- Step 2: How accurate is the STT?
- Step 3: How smart is the AI? How fast is the response time?
- Step 4: How natural does the voice sound?

Understanding the loop helps: debug problems, optimise performance, add features, understand other voice assistants.

---

## The 5 Components

1. **Wake word detection** — listens constantly, low CPU, only wakes on trigger
2. **STT** — converts audio to text, challenge is accents/noise/speed
3. **Language Model (Brain)** — understands and responds, challenge is speed + intelligence
4. **TTS** — converts response to speech, challenge is sounding natural
5. **Tools/Functions** — gives the assistant real abilities beyond chatting

---

## Old Design Decisions (No Longer Applying)

**Local-first approach** — original plan was fully local (no internet). New plan uses claw-code as brain which may require connectivity.

**FastAPI server architecture** — original plan was to build a FastAPI server with endpoints for each component (voice, STT, brain, TTS). This is a solid pattern worth revisiting if the project grows. More modular, easier to debug, easier to add a web UI later.

**Why FastAPI was chosen:**
- Test voice, TTS, brain separately via endpoints
- Can add web UI or mobile later
- Industry-standard, good software engineering practice
