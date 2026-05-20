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
1. **Agent-based testing** — test harness + Claude subagents to rigorously test SPIDy systematically
2. **Response latency** — Ollama brain still 5-8s to first sentence. Explore smaller fast model for casual replies
3. **Duplicate connections** — 42 nodes, obvious redundancy. Needs dedup pass
4. **"analyse ur systems"** — should actually read files + research improvements, not refuse
5. **Proactive commentary** — SPIDy should surface things unprompted without being asked
6. **Memory surfacing** — weave brain nodes into conversation naturally
7. **Screenshot/link intelligence** — read image/URL, extract facts, save to brain
8. See `SPIDy Roadmap.md` for full list

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
