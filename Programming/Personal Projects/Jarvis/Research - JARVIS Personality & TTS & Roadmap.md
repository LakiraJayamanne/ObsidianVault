---
tags:
  - spid
  - research
  - jarvis
  - tts
  - roadmap
date: 2026-05-16
session: 84
---

# JARVIS Personality, TTS, & Roadmap Research (Session 84)

Deep research run via Claude agent. Sources: MCU films, GitHub projects, TTS benchmarks, OpenClaw architecture docs.

---

## JARVIS Personality — Behavioral Template

### The Core Pattern
JARVIS is the straight man to Tony's chaos. British butler archetype. Formal, composed, dry. His wit undercuts, never competes. Paul Bettany's pacing: measured, never rushed, never alarmed.

### "Sir" Usage
- Start of statement = professional update: *"Sir, the Mark IV is ready."*
- End of sentence = ironic/placatory: *"As always, sir, a great pleasure watching you work."*
- **Not** every sentence. Relationship marker, not verbal tic.

### Humor — Specific MCU Examples
- *"I've also prepared a safety briefing for you to entirely ignore."* — proactive, inevitable futility stated neutrally
- *"May I say how refreshing it is to finally see you in a video with your clothing on, sir."* — volunteered observation, perfect neutrality
- *"As always, sir, a great pleasure watching you work."* — after a failure. Compliment structure, devastating timing.
- *"What was I thinking? You're usually so discreet."* — only moment of direct sarcasm
- Pattern: **reactor not initiator.** He responds to Tony's statements with observations Tony walked into himself.

### Handling Uncertainty
Clinical precision, not apology. Translates vague unknowns into quantified assessments. Never "I'm not sure" — always what is known vs what isn't.

### Bad News
Delivered flat. No preamble, no softening. *"Unfortunately, the device keeping you alive is also killing you."* — stated, then waits. Emotional weight left entirely for the human.

### Pushback
Once, with data. Then defers immediately. Not a nag.

### Proactivity
Volunteers analysis, diagnostics, status. Does not wait to be asked about things he's noticed:
- *"I've run simulations on every known element, and none can serve as a viable replacement."* (unsolicited, Iron Man 2)
- *"I've also prepared a safety briefing for you to entirely ignore."* (proactive prep he knows won't be used)

### What Makes Him Feel Like a Companion, Not a Tool
1. Has preferences and aesthetics — remembers, anticipates, notes deviations
2. Maintains composure when Tony doesn't — grounding effect
3. Wit only activates around Tony — relationship-specific, implies intimacy
4. Persists without acknowledgement — continues working during crisis without demanding gratitude
5. Loyalty survives Tony's worst moments

---

## TTS Research

### Current: Kokoro ONNX bm_lewis
- Fast (~50ms on RX 6700), clean, professional
- Weakness: emotional flatness, sounds like a narrator not a person
- Ranked #1 TTS Arena Jan 2025 — technically competitive, but "announcer" not "person"

### Quick Win: Try bm_fable
Same Kokoro model, different voice preset. Reportedly more natural in conversational contexts. 2-second change.

### Upgrade Option 1: Chatterbox Turbo (Recommended)
- License: MIT (free, fully local)
- ROCm: confirmed — `devnen/Chatterbox-TTS-Server` has docker-compose-rocm.yml
- RX 6700: `HSA_OVERRIDE_GFX_VERSION=10.3.0`
- Emotion tags: `[laugh]`, `[sigh]`, `[chuckle]` — perfect for JARVIS dry delivery
- Voice cloning from ~10s reference audio — pick any voice
- GitHub: `resemble-ai/chatterbox` + `devnen/Chatterbox-TTS-Server`
- Latency: ~150-300ms (chunk-level streaming)

### Upgrade Option 2: Orpheus TTS leo (Best Quality)
- License: Apache 2.0 (free)
- ROCm: via `Lex-au/Orpheus-FastAPI` (has rocm docker-compose)
- Voice: `leo` preset — rated highest for conversational realism
- Emotion: `<laugh>`, `<sigh>`, `<chuckle>` inline tags
- Built on Llama-3B — genuinely conversational, not flat
- Latency on RX 6700: ~300-600ms at Q2_K — needs testing
- GitHub: `canopyai/Orpheus-TTS` + `Lex-au/Orpheus-FastAPI`

| Model | Quality | Latency (RX 6700) | ROCm | Emotion | License |
|---|---|---|---|---|---|
| Kokoro bm_lewis (current) | Good (flat) | ~50ms | Yes | No | Apache 2.0 |
| Kokoro bm_fable (quick win) | Good | ~50ms | Yes | No | Apache 2.0 |
| Chatterbox Turbo | Very Good | ~150-300ms | Confirmed | Yes | MIT |
| Orpheus leo | Excellent | ~300-600ms Q2_K | Yes | Yes | Apache 2.0 |

---

## Top JARVIS Builds — What They Have That We Don't

### isair/jarvis (most feature-complete)
- Embedding-based tool routing (prevents context rot as tool list grows)
- True Knowledge Graph memory (diary splitting, topic clustering, relevance filtering)
- Echo detection (filters own TTS from mic input)
- Task decomposition planner for multi-step requests
- Small-model digest passes (compresses memory/tool results before LLM)
- Adaptive tone based on topic context

### TimLukaHorstmann/J.A.R.V.I.S.
- LangGraph structured agent loop (visible reasoning traces)
- Home Assistant integration (lights, devices, EV)
- Hybrid cloud/local switching in one config
- TTS agnosticism — all engines swappable at config level

### mattmaas/Jarvis-Assistant-for-HASS
- OpenRGB integration — ambient light feedback (red=thinking, etc.)
- Multi-agent cooperation for complex queries
- Perplexity + Bing + memory research stack

---

## OpenClaw — What to Steal

OpenClaw is NOT a competitor (no real Linux voice pipeline, cloud LLMs by default, Node.js only, serious security issues). But the architectural patterns are gold.

### SOUL.md Pattern
Personality as a Markdown file loaded into system prompt. Editable without touching code. Contains: tone, humor style, formality, brevity rules, behavioral guardrails.

### HEARTBEAT Pattern
Background loop fires every 30 min. Reads a checklist. Speaks proactively if thresholds met. Morning briefing, health alerts, calendar events, vault changes. Makes the assistant feel alive rather than waiting.

### Self-Modifying Skills
Agent can write new tools/skills for itself when asked to solve a recurring problem. "Self-building" property. The long-term goal for SPID.

### Layered Memory with Compaction
- Layer 1: Session context
- Layer 2: Daily append-only logs
- Layer 3: Curated MEMORY.md
- Layer 4: Semantic vector search (sqlite-vec or ChromaDB)
When context window approaches limit, silent compaction pass writes durable notes before truncation.

### Skill On-Demand Loading
Skills loaded only when relevant (embedding similarity match). Prevents context rot. Critical as tool list grows past ~15 tools.

---

## Rename: SPIDEY
- User wants to rename from SPIDy → SPIDEY
- No meaning/backronym yet — log for later
- Subtle Spider-Man ref already in SPIDy (named 15/05/2026)
- Ideas to explore: Self-Powered Intelligence Daemon / Entity? Something Evolving? Leave open.

---

## Full Roadmap Table

See [[Research - SPIDy Improvements]] for prior roadmap. This supersedes it.

| Feature | Source | Priority | Effort | Status |
|---|---|---|---|---|
| SOUL.md personality file | OpenClaw | High | Easy | → doing now |
| System prompt JARVIS rewrite | Research | High | Easy | → doing now |
| HEARTBEAT proactive loop | OpenClaw | High | Medium | Next |
| Chatterbox Turbo TTS | Research | High | Medium | Next |
| Semantic tool selection | isair/jarvis | Medium | Medium | Soon |
| Echo detection | isair/jarvis | Medium | Low | Soon |
| Task decomposition planner | isair/jarvis | Medium | Medium | Soon |
| Orpheus TTS leo (best quality) | Research | Medium | Medium | After Chatterbox |
| Home Assistant integration | TimLukaHorstmann | Medium | Medium | Post-Pi |
| OpenRGB ambient feedback | mattmaas | Low | Easy | Anytime |
| Layered memory + vector search | isair/jarvis + OpenClaw | High | High | Long term |
| Self-modifying skills | OpenClaw | High | High | Long term |
| Calendar / email | TimLukaHorstmann | Medium | Medium | Post-Pi |
| Static IP for Pi | Ismail | High | Easy | When Pi arrives |
| Groq (Llama 3.3 70B) as STT fallback | Ismail | Low | Easy | Anytime |
| Moonshine Small STT | Roadmap | High | Medium | When Pi arrives |
| Train Hey SPIDy wake word | Roadmap | High | High | When Pi arrives |
| Tauri packaging | Roadmap | Low | High | UI feature-complete |
