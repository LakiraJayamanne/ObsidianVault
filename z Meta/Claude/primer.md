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

## SPID — Self-hosted Personal Intelligence Daemon 🔥

**Named 15/05/2026. Pronounced "Spidy" — subtle Spider-Man reference.**

### Session 92 — COMPLETED (20/05/2026, ~14:21–15:15 BST)

#### Done this session
- **Brain graph — full tree layout** (core → cluster hubs → leaf nodes)
  - Force simulation replaced with radial tree: goldenSphere for hubs (r=3.4), sub-spheres for nodes (r=1.1)
  - Edges rendered as batched THREE.LineSegments (core→hub white, hub→node cluster-colored)
  - Cluster hub meshes with labels + node count, colored per cluster
  - SPIDY label on central core
  - Per-node organic drift animation (no GC pressure)
  - Camera pulled back to z=13
- **No more 10-second simulation reset** — nodeIdKey memo, drift data stable across polls
- **Performance fix** — pre-allocated scratch Vector3s (_s1, _s2), eliminated ~150 allocs/frame
- **Silent text mode** — `_respond_silent()` in main.py, text queries show in chat without TTS
- **OTHER cluster fix** — TYPE_CLUSTER fallback: connection→CONNECTIONS, observation→RESEARCH, reflection→HEADSPACE
- **Gender fix** — deleted nodes b13ac518 ("Lakira is female") and 5b6d0c57 ("her dad"), added correct ones; identity lock + memory filter now explicitly say MALE
- **Pronoun fix** — soul.md HARD RULES: always "you/your" when speaking to Lakira directly
- **Web search fallback** — falls back to web_research() when DDG instant answers return nothing
- **Games node updated** — 3ffe97eb → cc4706ef: Deadlock, The Finals, Crimson Desert
- **Self-code modification** — 4 new tools in tools.py:
  - `read_own_source(filename)` — read any source file
  - `edit_soul(new_content)` — rewrite soul.md (validated, auto-backup)
  - `set_config(key, value)` — tune humour/sarcasm/conversation_silence live
  - `propose_code_change(filename, description, old, new)` — saves proposal to proposals/ for Lakira review
- **Git commit**: 1263f88

#### Current state of brain
- 66 nodes total (IDENTITY, FITNESS, GAMING, MEDIA, EDUCATION, ROUTINE, TECH, PROJECTS, HEADSPACE, FAMILY, CONNECTIONS, RESEARCH)
- Autonomous connections firing every 5min
- Proactive research every 30min (some noise — Brawl Stars rankings, Yeat facts mixed with irrelevant medical/cat nodes)
- Soul tuning every 60min

### Remaining / Next up
1. **Clean research branch** — delete garbage nodes (Cheeseball wizard cat x2, Aβ seeding, brain metastasis). Tighten proactive_research query to stay on topic
2. **Self-code mod testing** — try "read your soul file", "be funnier", "propose a change to yourself"
3. **Fix "OTHER" cluster** — a few nodes may still be gray
4. **Firing animation** — verify node flash is visible on voice queries
5. **Proactive research quality** — currently finds irrelevant stuff, needs better seed→query logic

### Full architecture doc
`Programming/Personal Projects/Jarvis/Homelab & JARVIS Architecture.md`

### Current stack
| Component | Choice |
|---|---|
| Wake word | hey_jarvis_v0.1.onnx |
| STT | Moonshine BASE (~300-500ms) |
| Brain | qwen3:8b (jarvis-brain Modelfile) on RX 6700 |
| TTS | Chatterbox Turbo (voice queries only) |
| Memory | ChromaDB + vault at `z Meta/SPIDy/brain/` |
| UI | Next.js, React, Three.js, Framer Motion |

---

## GroundLink Sri Lanka — DAD REVIEW IN PROGRESS 🔥 PRIORITY #1
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
1. **SPIDy research branch cleanup + proactive research quality**
2. **SPIDy self-code mod testing**
3. **GroundLink** — awaiting dad's feedback
