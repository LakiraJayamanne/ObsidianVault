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

### Brain system — BUILT ✓ (session 88, 20/05/2026)

**Memory reset done** — old brain wiped. New architecture:
- `memory.py` — ChromaDB persistent vector DB + vault .md files
- 4 types: fact, observation, reflection, connection
- Each memory stored at `z Meta/SPIDy/brain/<type>/` in vault AND embedded in ChromaDB
- SPIDy writes his own memories via `remember` tool
- Every query fires ChromaDB search → matching nodes light up white on MemoryGraph (neurons)
- `_extract_and_save` filter tightened — only saves explicit personal facts stated by the user. Not hallucinated traits, not conversation mechanics.

**MemoryGraph** — shows SPIDy's brain (NOT Obsidian vault). Color-coded by type:
- facts = red, observations = orange, reflections = blue, connections = green
- Idle rings: faint orbit rings shown only for types that have nodes
- Thinking rings: full atom orbit, only shown when 4+ nodes exist
- Polls `/api/brain` every 10s

**Autonomous connections** — live in `proactive.py`, fires every 600s when brain has 2+ memories. Picks 2-3 random memories, finds a connection with LLM, saves as `connection` node, fires neurons on graph.

**Brain-filling questions** — in `brain.py`. When user says "ask me questions / fill your brain / what do you want to know", SPIDy generates one targeted question based on memory gaps. User's answer flows through `_async_remember` automatically.

### Personality — WORKING ✓ (session 88)
- soul.md loaded correctly, identity lock hardened
- Knows name is Lakira (not Lakshmi) — hardcoded in `_IDENTITY_LOCK`
- Banned phrases: "How can I assist you today?", "How can I help?", etc.
- Max 2 sentences enforced
- `_SOUL_PRIMER` removed (was causing "first time speaking" contradiction)
- Modelfile rebuilt: `jarvis-brain` from `qwen3:8b`, `num_ctx 4096`, identity lock in SYSTEM

### Current stack
| Component | Choice |
|---|---|
| Wake word | hey_jarvis_v0.1.onnx |
| STT | Moonshine BASE (~300-500ms) |
| Brain | qwen3:8b (jarvis-brain Modelfile) on RX 6700 |
| TTS | Chatterbox Turbo (3.3s/sentence — ROCm GEMM issue, known) |
| Memory | ChromaDB + vault at `z Meta/SPIDy/brain/` |

### UI — NEXT 🔥
- **Design direction agreed:** HUD-style + Apple glass hybrid. Black (#080808) + deep crimson (#C0001A)
- **Stack:** Next.js + Tailwind + Framer Motion
- **WHERE:** `/home/lakira/Documents/Projects/SPIDy/ui/`
- UI revamp is the NEXT thing to build after brain is verified

### Still pending (small)
- Verify `_async_remember` saves correctly after play/pause intent fix (re-test "go to the gym, play a game..." answer)
- 8-item test list from session 85 still mostly untested (lower priority now)

### Planned but not built
- Background autonomous connections ✓ BUILT (session 88)
- Proactive brain-filling questions ✓ BUILT (session 88)

### Files changed this session (uncommitted)
- `brain.py` — identity lock, soul primer removed, brain-fill, _async_remember filter, multi-step threshold 3
- `tools.py` — _ABOUT_FILE dead code removed
- `proactive.py` — autonomous connections trigger added
- `intent.py` — play/pause patterns tightened (no longer triggers on "play a game")
- `Modelfile` — rebuilt, num_ctx 4096, stronger identity lock
- `memory.py` — new file (ChromaDB brain)
- `ui/app/components/MemoryGraph.tsx` — brain polling, orbit ring fixes, idle rings
- `ui/app/components/SystemPanel.tsx` — /api/vault → /api/brain
- `ui/app/api/brain/route.ts` — new file

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
1. **SPIDy UI revamp** — next session
2. **GroundLink** — awaiting dad's feedback
3. **SPIDy — remaining 8-item test list** — lower priority
