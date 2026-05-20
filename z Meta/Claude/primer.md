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

### UI — DONE ✓ (session 90, 20/05/2026)

**Full redesign completed. Stack: Next.js, React, Framer Motion, Three.js**

**Design: dark glassmorphism, black & white accent, JetBrains Mono throughout**

- Background: animated nebula breathing (CSS keyframes)
- Panels: dark glass `rgba(10,10,12,0.54)`, left crimson→white accent bar for section labels, 4px stat bars with glowing leading edge
- MemoryGraph: nodes white (#DEDEDE), TYPE_COLOR → white opacity variants, orbit rings white
- StatusPill: dot/pulse/sequential-dots by mode, white glow
- VoiceBar: idle dot → 16 animated waveform bars on listening/speaking
- Terminal: scanline texture overlay
- HealthPanel + SystemPanel: fully redesigned, large display numbers
- TextChat: centered glass chat panel (640px), user bubbles right, SPIDy left with dot avatar, thinking indicator, top fade gradient, dims sidebars + graph to 15%
- Toggle: `T` button next to VoiceBar, `⌥` dev controls

### Next up
1. **Brain seeder script** — bulk-load `about-lakira.md`, `tech-setup.md`, `projects.md` from vault into ChromaDB as fact nodes. SPIDy goes from ~1 node to ~50 overnight.
2. **Proactive web research** — SPIDy autonomously researches topics related to existing memories on a timer (similar to autonomous connections)
3. **Autonomous connections live test** — needs 10min runtime + 2+ memories

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
1. **SPIDy brain seeder** — next task this session
2. **GroundLink** — awaiting dad's feedback
3. **SPIDy proactive web research** — after seeder
4. **SPIDy autonomous connections live test** — lower priority
