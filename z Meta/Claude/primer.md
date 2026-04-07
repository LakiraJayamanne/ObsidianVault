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
- **Ollama** — Installed, llama3.1 8B pulled and working ✓
- **Voice Assistant (JARVIS)** — IN PROGRESS ⚠️
  - config.py ✓
  - tts.py ✓ (tested, working)
  - brain.py — in progress (imports done, think() function shell written, ollama.chat() call next)
  - stt.py — not started
  - wake.py — not started
  - main.py — not started
  - input.py — not started
- **Gym Tracker** — Phase 1 complete. Phase 2 not started.
- **Memory system** — Fully in Obsidian vault ✓

## Voice Assistant — Current Stack
| Component | Choice |
|---|---|
| Wake word + snaps | OpenWakeWord (fully local, no account needed) |
| STT | Whisper (local) |
| Brain | Ollama — llama3.1 8B |
| TTS | edge-tts — en-GB-RyanNeural |
| Text input | Terminal + WhatsApp (planned) |

- Wake word: "Persona" (two snaps also planned as alternative trigger)
- Assistant name: **JARVIS** (placeholder — will rename to a Persona game character later)
- Project at: `/home/lakira/Documents/Projects/MyPersona/`
- Full build notes: `Programming/Personal Projects/Jarvis/Persona Build Notes.md`

## GRUB State (desktop) — needs cleanup
- Theme: DISABLED (Valhalla caused silent black screen)
- GRUB_TERMINAL_OUTPUT=console (text mode)
- GRUB_CMDLINE_LINUX="nomodeset" — still present, should be removed
- Only one kernel: 6.19.10-200.fc43 (6.17.1 removed ✓)
- Goal: remove nomodeset, switch to gfxterm, apply Gorgeous-GRUB Matrix/Morpheus theme (Fedora + Windows version)

## Priority Order (next session)
1. **Finish brain.py** — write ollama.chat() call, test it
2. **stt.py** — Whisper STT
3. **wake.py** — OpenWakeWord
4. **input.py** — terminal text input
5. **main.py** — tie everything together
6. **GRUB theme** — Gorgeous-GRUB, remove nomodeset
7. **Plymouth boot animation**
8. **Gym Tracker Phase 2**
9. **Guide Tracker app** (for Lakira's dad, Windows)

## Caelestia Notes (desktop)
- Installed via EnceladusII/caelestia-fedora (abandoned Fedora fork, frozen Aug 2025)
- Quickshell installed via COPR (errornointernet/quickshell)
- Shell lives at ~/.config/quickshell/caelestia
- Hyprland config split across ~/.config/hypr/hyprland/*.conf
- User overrides go in ~/.config/caelestia/hypr-vars.conf and hypr-user.conf
- Keybinds at ~/.config/hypr/hyprland/keybinds.conf
- Bar is on the left (default)

## Laptop Plan (keep Waybar — iGPU can't handle full Quickshell bar)
- Tighten island layout, pill workspaces
- Add 1-2 lightweight Quickshell popups (music, calendar)
- Upgrade matugen pipeline to MatugenColors.qml live polling
- Configure Hypridle
- Keep Persona blade menu on laptop only

## Already Working on Laptop (don't redo)
- `Super+Q` → Persona Quickshell blade menu (POWER/STATS/CLAUDE)
- `Super+W` → wallpaper picker
- `Super+Shift+W` → cycle wallpaper
- `Super+Ctrl+B` → waybar style switcher
- `Super+Alt+B` → waybar layout switcher
- `Super+L` → hyprlock
- `Super+E` → Nautilus
- Power button left-click → wlogout
- `Super+D` → rofi app launcher
- `Super+Tab` → rofi window switcher
- Fish + spidey oh-my-posh prompt + fastfetch on startup
- Dynamic theming via matugen
- Dynamic papirus folder colors

## Game Setup Notes (laptop)
- Undertale: `bash /home/Lakira/Games/Undertale/launch.sh` (needs DISPLAY=:0, fuse-overlayfs)
- Wine+DXVK: `DISPLAY=:0 WINEDLLOVERRIDES="d3d11,dxgi=n" wine game.exe`
- jc141 native builds: need fuse-overlayfs, run start.n.sh from within game directory
- FitGirl repacks: `DISPLAY=:0 wine setup.exe`, install to ~/Games/
- Omori: IGG Windows build + Wine → ~/Games/OMORI
- Ender Magnolia: FitGirl + winetricks vcrun2022

## Gym Tracker Build Phases
1. [x] Phase 1 — models.py (ExerciseSet, Session, Log)
2. [ ] Phase 2 — storage.py (save/load JSON)
3. [ ] Phase 3 — main.py (text menu)
4. [ ] Phase 4 — algorithms.py (overload, plateau, bodyweight trend)
5. [ ] Phase 5 — Polish

## Gym Data Logged So Far
- Session 1: Pull Day — 17/03/2026 — BW 71kg
- Session 2: Push Day — 20/03/2026 — BW 72kg (clothes, no shoes)

## Desktop Only
- **Guide Tracker app** — project for Lakira's dad, Windows desktop only.

## ilyamiro/nixos-configuration — Key Patterns Worth Stealing
1. Morphing master window
2. MatugenColors.qml live-polling
3. Focus time daemon (Python + SQLite)
4. DDG wallpaper search in picker
5. Calendar time-of-day color mapping
6. Workspace pills with staggered startup animation
7. Custom lock screen QML with Quickshell.Services.Pam
8. Plymouth: 80-frame animation + 80-frame progress sequence
