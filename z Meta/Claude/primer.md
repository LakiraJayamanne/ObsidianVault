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

- `memory.py` — ChromaDB persistent vector DB + vault .md files
- 4 types: fact, observation, reflection, connection
- Each memory stored at `z Meta/SPIDy/brain/<type>/` in vault AND embedded in ChromaDB
- SPIDy writes his own memories via `remember` tool
- Every query fires ChromaDB search → matching nodes light up white on MemoryGraph (neurons)
- `_extract_and_save` — FIXED: dedup check was always false (load_memory() with no query returns ""). Fixed to load_memory(fact). Error handling fixed (was silently swallowed, now prints errors).
- Vault + ChromaDB sync confirmed working. Orphaned vault files cleaned up.
- Brain-fill questions working (_generate_brain_question)
- Autonomous connections wired (proactive.py, 600s timer) — code verified, not yet tested live

### Current stack
| Component | Choice |
|---|---|
| Wake word | hey_jarvis_v0.1.onnx |
| STT | Moonshine BASE (~300-500ms) |
| Brain | qwen3:8b (jarvis-brain Modelfile) on RX 6700 |
| TTS | Chatterbox Turbo (3.3s/sentence — ROCm GEMM issue, known) |
| Memory | ChromaDB + vault at `z Meta/SPIDy/brain/` |

### UI — IN PROGRESS 🔥

**Design direction: sleek glassmorphism — dark, translucent panels, smooth animations**

**Session 89 UI changes (partial revamp — SCRAPPED, starting fresh):**
- Removed corner Brackets, removed "SYSTEM //" headers from all panels
- Rounded corners (14px) on all panels
- New glass style: `rgba(13,13,17,0.38)` + `blur(28px)` + white border
- 3px gradient stat bars
- VoiceBar → pill shape (border-radius 50px)
- StatusPill → proper pill (border-radius 9999px)
- MemoryGraph: nodes 0.04→0.10, central core 0.1→0.13, bloom 1.4→0.4, orbit rings 0.06→0.15, idle breathing animation, fire flash white spike
- Background: attempted radial gradient glows — not satisfying

**NEXT: Full UI restart using `/frontend-design` skill**
- Lakira scrapped the partial revamp and wants a clean redesign using the frontend-design skill
- Design brief: sleek glass look, lots of translucency, smooth comfortable animations, everything flows
- frontend-design skill installed at `~/.claude/skills/frontend-design/SKILL.md`
- Start fresh next session with the skill active

### Still pending (small)
- Autonomous connections test live (needs 10min wait + 2+ memories in ChromaDB)
- MemoryGraph visual confirmation with multiple node types

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
1. **SPIDy UI full redesign** — next session, use /frontend-design skill
2. **GroundLink** — awaiting dad's feedback
3. **SPIDy — autonomous connections live test** — lower priority
