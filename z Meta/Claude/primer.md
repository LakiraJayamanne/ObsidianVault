---
tags:
  - claude-memory
  - claude/status
---

# Project Primer

Current project status, what's in progress, what's next.

---

## Current Status
- **Hyprland on Fedora (laptop)** — Fully working. SDDM fixed. ✓
- **Desktop dual boot (Fedora 43)** — DONE ✓ (02/04/2026)
- **Desktop Hyprland + Caelestia rice** — FULLY WORKING ✓ (07/04/2026)
- **Ollama** — llama3.1 8B + llama3.2:3b pulled, 100% GPU via ROCm ✓
- **Desktop GRUB** — Text mode, nomodeset still in kernel args. Theme NOT yet applied. ⚠️

---

## SPIDy — Self-hosted Personal Intelligence Daemon 🔥

**Named 15/05/2026. Pronounced "Spidy" — subtle Spider-Man reference.**

### Session 94 — COMPLETED (20/05/2026, ~18:57–19:55 BST)

#### Done this session
- **Full test harness built** — 173 tests across 2 rounds: intent routing, noise filter, tool smoke tests, brain regex patterns, memory system, vault note tools, health data tools, multi-step decomposition, heartbeat logic, soul tuning, autonomous connections, proactive research, focus mode, end-to-end live WS tests.
- **Bug: BRAIN_FILL_RE pattern gap** — "what would you like to ask" wasn't matching. Added `would you` + `like` variants. Fixed.
- **Bug: Memory recall truncated at 80 tokens** — recall queries shared the tool-decision LLM call (80-token cap). Now streams directly with 300 tokens. Full uncut responses.
- **Bug: Connection dedup used word overlap** — 60% word overlap missed semantic duplicates with synonyms (58% = miss). Switched to ChromaDB embedding distance < 0.30. Far more robust.
- **Feat: Personality-driven autonomy responses** — soul tuning flagged "On it." as too generic. Now picks from 5 JARVIS-style lines with character.
- **Git commits**: d2a0fd4, 6c64c98, d9fa6f2

#### Current state of brain
- ~115 nodes (facts + connections + observations — proactive research added 2 this session)
- Soul self-wrote a tuning note: "do ur thing response could be more playful" → actioned
- Dedup now uses semantic distance — more connections will be caught and skipped correctly

### Session 93 — COMPLETED (20/05/2026, ~17:50–18:55 BST)

#### Done this session
- **TTS swap: Chatterbox → Piper** — ~130ms/sentence vs 3-8s. Frees ~3GB VRAM for Ollama. Voice: en_GB-alan-medium.
- **Soul file force-route** — `intent.py` now hard-routes "read/show your soul/brain/config/..." directly to `read_own_source`, bypassing LLM refusal entirely. `[fast]` log confirms it works.
- **web_research URL fix** — DDG link extraction was broken (wrong anchor parser). Replaced with `uddg=` regex, matches proactive.py approach.
- **Autonomy mode** — "do ur thing / research freely / ur free to" → says "On it." + immediately fires `_proactive_research()` in thread. No more passing phrase as a search query.
- **Soul: AUTONOMY section** — explicit instruction that SPIDy has its own agenda, doesn't refuse or call things redundant, takes initiative when given space.
- **Research: SKIP mechanism** — query generator now returns SKIP for physical object seeds (posters, decorations). Prevents wizard cat → lore research loops.
- **Garbage node cleanup** — deleted 12 nodes total: 8 from last session (wizard cat x2, Glydde x2, Aβ seeding, brain metastasis, Brawl Stars x2) + 4 this session (wizard cat poster x2, bad connection, Cheeseball meme).
- **Roadmap saved** — `Programming/Personal Projects/Jarvis/SPIDy Roadmap.md` in vault.
- **Git commits**: a733f6f, a79d1b6, 9e87a26, 4f23d30, daec91d, 6ca7c21

#### Current state of brain
- 110 nodes (51 facts, 42 connections, 14 research observations + 3 new)
- Autonomous connections firing every 5min (dedup working well)
- Proactive research every 30min (now skips physical object seeds)
- Soul tuning every 60min
- All clusters rendering correctly in tree layout

### Current stack
| Component | Choice |
|---|---|
| Wake word | hey_jarvis_v0.1.onnx |
| STT | Moonshine BASE (~300-500ms) |
| Brain | qwen3:8b (jarvis-brain Modelfile) on RX 6700 |
| TTS | **Piper en_GB-alan-medium (~130ms, CPU)** |
| Memory | ChromaDB + vault at `z Meta/SPIDy/brain/` |
| UI | Next.js, React, Three.js, Framer Motion |

### Next up (priority order)
1. **Response latency** — Ollama brain still 5-8s to first sentence. Explore smaller fast model for casual replies
2. **Proactive commentary** — SPIDy should surface things unprompted without being asked
3. **Memory surfacing** — weave brain nodes into conversation naturally
4. **Screenshot/link intelligence** — read image/URL, extract facts, save to brain
5. See `SPIDy Roadmap.md` for full list

---

## GroundLink Sri Lanka — DAD REVIEW IN PROGRESS 🔥
- **What it is:** SaaS platform for guide/driver/vehicle management in Sri Lankan inbound tourism
- **Client:** TTC Sri Lanka (dad's company — laahiru@ttcsrilanka.com)
- **Project path:** C:\Users\lakir\Documents\Projects\groundlink
- **GitHub:** https://github.com/LakiraJayamanne/groundlink (private)
- Phase 1 complete. Awaiting dad's feedback before Phase 2.

---

## CO1109 Enron Assignment — SUBMITTED ✓ (27/04/2026 1:30am)
## OOP Test — COMPLETED (13/05/2026)

---

## Priority Order
1. **SPIDy — agent testing + latency + autonomy improvements**
2. **GroundLink** — awaiting dad's feedback
