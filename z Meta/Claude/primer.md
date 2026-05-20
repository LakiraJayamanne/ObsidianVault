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
  - rgba syntax fixed, keybinds working, quickshell bar working
  - Dynamic Material You theming active
  - Vibrance shader active (1.1x saturation) at ~/.config/hypr/shaders/vibrance.frag
  - Mouse accel disabled
  - Super+Backspace + Super+middle click = killactive
  - Super+Shift+W = wallpaper shuffle
  - Sidebar character = spidey_circle.png
  - fastfetch = saturn.txt logo (image attempts abandoned due to sixel black bar issue)
- **Desktop GRUB** — Text mode (console), old kernel removed (6.17.1 gone, only 6.19.10 remains), rescue entry hidden. Theme NOT yet applied. nomodeset still in kernel args. ⚠️
- **Desktop Windows boot fix** — CONFIRMED WORKING ✓
- **Monitor @ 165Hz, scale 1.0** — Set in ~/.config/hypr/hyprland/monitors/default.conf ✓
- **Zen Browser** — Installed via Flatpak ✓
- **Spicetify** — DONE ✓
- **Wallpapers** — Synced from laptop ✓
- **Ollama** — llama3.1 8B + llama3.2:3b pulled, 100% GPU via ROCm (HSA_OVERRIDE_GFX_VERSION=10.3.0 in systemd override) ✓
- **System font** — Segoe UI (copied from Windows partition), set via gsettings + GTK3/4 ✓
- **Mouse sensitivity** — flat accel, sensitivity -0.15 ✓
- **Apple Watch (Series 3)** — Dad's old watch, set up with Omnitrix photo face. Battery degraded (~3hrs). watchOS 8.8.1, no jailbreak possible. Clockology not compatible. Decent for step tracking/notifications as-is.
- **Workspace move keybind** — Super+Alt+[number] (Caelestia default, confirmed from hyprconfig)

---

## SPID — Self-hosted Personal Intelligence Daemon 🔥

**Named 15/05/2026. Pronounced "Spidy" — subtle Spider-Man reference.**

### Brain system — FULLY WORKING ✓ (session 89, 20/05/2026)

- `memory.py` — ChromaDB persistent vector DB + vault .md files. add(), search(), all_memories(), delete() functions.
- 4 types: fact, observation, reflection, connection
- Each memory stored at `z Meta/SPIDy/brain/<type>/` in vault AND embedded in ChromaDB
- `_extract_and_save` — FIXED: dedup check was always false. Error handling fixed.
- Vault + ChromaDB sync confirmed working.
- Brain-fill questions working (_generate_brain_question)
- Tags stored in frontmatter and returned by brain API

### Autonomous features (session 91, 20/05/2026)
- `seed_brain.py` — bulk-loaded 49 facts from vault into ChromaDB. 52 total nodes.
- `_autonomous_connections` in proactive.py — fires every 5min, semantic seed+neighbor clustering, produces non-obvious insights
- `_proactive_research` in proactive.py — fires every 30min, picks random memory, DDG search, extracts 1-2 obs facts
- `_soul_tuning` in proactive.py — fires every 60min, reviews last 12 exchanges, appends self-observation to soul.md (max 5 notes)
- brain.py: `_SELF_RECALL_RE` — "tell me everything about me" triggers all_memories() path, no 2-sentence limit
- Wrong "Coventry University" nodes deleted. Correct "University of Leicester" node confirmed.

### Current stack
| Component | Choice |
|---|---|
| Wake word | hey_jarvis_v0.1.onnx |
| STT | Moonshine BASE (~300-500ms) |
| Brain | qwen3:8b (jarvis-brain Modelfile) on RX 6700 |
| TTS | Chatterbox Turbo (3.3s/sentence — ROCm GEMM issue, known) |
| Memory | ChromaDB + vault at `z Meta/SPIDy/brain/` |

### UI — Updated ✓ (session 91, 20/05/2026)

**Stack: Next.js, React, Framer Motion, Three.js**
**Design: dark glassmorphism, JetBrains Mono throughout**

- MemoryGraph: force-directed 3D layout, cluster labels (IDENTITY/FITNESS/GAMING etc.), colored nodes per cluster, no edges
- Cluster colors: blue=Identity, mint=Fitness, orange=Gaming, purple=Media, cyan=Education, amber=Routine, pink=Projects, teal=Connections, lime=Research
- StatusPill, VoiceBar, TextChat all working
- TextChat: T button toggle, sidebars dim to 15%

### Remaining / Next up
1. **Self-code modification** — SPIDy reading and editing his own code (ambitious, needs guardrails)
2. **Fix "OTHER" cluster** — nodes with unrecognized tags falling into gray OTHER bucket
3. **Firing animation visibility** — verify node flash is visible on query
4. **Games list outdated** — need to update `3ffe97eb` node with current games

### Full architecture doc
`Programming/Personal Projects/Jarvis/Homelab & JARVIS Architecture.md`

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
1. **SPIDy self-code modification** — next ambitious feature
2. **GroundLink** — awaiting dad's feedback
3. **SPIDy misc fixes** — OTHER cluster, games node update
