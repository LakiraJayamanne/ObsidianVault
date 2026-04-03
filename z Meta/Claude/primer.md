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
- **Desktop GRUB** — DONE ✓ (03/04/2026) — Valhalla theme active, 10s timeout, Windows 11 entry present, Fedora entry renamed to "Fedora". menu_auto_hide unset from grubenv — was silently skipping menu on cold boot.
- **Desktop Windows boot fix** — Fixed (03/04/2026) — GRUB entry was pointing to NTFS UUID (5A728A6A728A4B29) instead of EFI partition UUID (D289-BBA0). Fixed 40_custom to use correct UUID + insmod fat/part_gpt. grub2-mkconfig rebuilt. Untested — confirm Windows boots on next reboot.
- **Gym Tracker** — Phase 1 complete. Ready to start Phase 2 (storage.py).
- **Memory system** — Fully migrated to Obsidian vault (z Meta/Claude/). ✓
- **Obsidian vault** — Main base for Claude memory. Synced to GitHub (ObsidianVault repo). ✓
- **Voice Assistant** — Stack decided. Not started. Waiting on desktop setup.

## Memory System — How It Works
- All memory lives in the vault at `z Meta/Claude/`
- Claude reads `lessons.md`, `primer.md`, `session-log.md` at session start
- Claude writes/commits/pushes the ObsidianVault repo at session end
- Obsidian Git plugin removed — Claude handles git
- Old `claude-memory` repo to be archived (both machines now confirmed on vault)

## In Progress
- **Desktop Hyprland setup** — GRUB fully done, next: install Hyprland on desktop
- **Desktop rice plan** — Hyprland first, then claw-code + Ollama, then caelestia rice
- **Voice Assistant** — stack locked, build starts after desktop is set up

## Priority Order
1. **Desktop Hyprland install** ← next
2. **claw-code + Ollama** — set up as Claude Code cooldown fallback BEFORE ricing
3. **Desktop rice** — caelestia + ilyamiro widgets
4. **Voice assistant** — build starts after above three

## GRUB Notes (desktop)
- Theme: YouStones/ultrakill-revamp-grub-theme — installed to /boot/grub2/themes/ultrakill-revamp-grub-theme/
- GRUB_TERMINAL_OUTPUT="gfxterm" is commented out — if theme renders broken, uncomment and rebuild
- Fast Boot disabled in BIOS ✓ (03/04/2026) — GRUB now shows on warm reboot

## Voice Assistant — Stack Locked (01/04/2026)
| Component | Choice |
|---|---|
| Wake word | Porcupine (Picovoice) — wake word name TBD |
| STT | Whisper (local) |
| Brain | claw-code |
| TTS | edge-tts |

- Cross-platform: Windows + Linux
- Don't build/test on laptop — iGPU can't handle Whisper well. Use desktop (RX 6700XT).
- Old JARVIS project notes archived in vault at `Programming/Personal Projects/Jarvis/Old Notes (Aug 2025).md`

## Desktop Setup Order (planned)
1. Fedora dual boot + Hyprland base ← **next**
2. claw-code + Ollama — set up BEFORE ricing
3. Caelestia as the base shell (elegant, Material You, fish-native, better Qt/GTK integration)
4. Port ilyamiro widgets into caelestia — music EQ popup, DDG wallpaper search, focus time tracker
5. Plymouth boot animation (reference ilyamiro's 80 frames)

## Laptop Plan (keep Waybar — iGPU can't handle full Quickshell bar)
- Tighten island layout, pill workspaces
- Add 1-2 lightweight Quickshell popups (music, calendar) using ilyamiro's morphing master window pattern
- Upgrade matugen pipeline to MatugenColors.qml live polling (no more waybar restarts)
- Configure Hypridle (still not done)
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
- hyprpolkitagent running
- Waybar wallpaper widget: left click cycles, right click opens picker
- Bibata-Modern-Ice cursor active
- Dynamic theming via matugen (wallpaper → colors → waybar, kitty, rofi, hyprlock, wlogout, btop, gtk, cava)
- Dynamic papirus folder colors via papirus-dynamic.sh

## Game Setup Notes (laptop)
- Undertale: `bash /home/Lakira/Games/Undertale/launch.sh` (needs DISPLAY=:0, fuse-overlayfs)
- Wine+DXVK: `DISPLAY=:0 WINEDLLOVERRIDES="d3d11,dxgi=n" wine game.exe`
- jc141 native builds: need fuse-overlayfs, run start.n.sh from within game directory
- FitGirl repacks: `DISPLAY=:0 wine setup.exe`, install to ~/Games/
- Omori: IGG Windows build + Wine → ~/Games/OMORI
- Ender Magnolia: FitGirl + winetricks vcrun2022, desktop file at ~/.local/share/applications/

## ilyamiro/nixos-configuration — Key Patterns Worth Stealing
1. Morphing master window (single qs-master FloatingWindow, teleport + resize + StackView swap)
2. MatugenColors.qml live-polling (/tmp/qs_colors.json, every 1s)
3. Focus time daemon (Python + SQLite, per-app active window tracking)
4. DDG wallpaper search integrated into picker (streams results via get_ddg_links.py)
5. Calendar time-of-day color mapping (peach=morning, sapphire=afternoon, mauve=evening, blue=night)
6. Workspace pills with staggered startup animation (index×60ms delay)
7. Custom lock screen QML with Quickshell.Services.Pam (not hyprlock)
8. Plymouth: 80-frame animation + 80-frame progress sequence (PNGs)

## MP3 Player (shortlisted as of 30/03/2026)
- SUPEREYE 32GB — £14.99 + £2.95 delivery, eBay, built-in storage
- HiFi Walker H2 — auction, ~£21.50, Rockbox DAP, better audio, likely needs microSD

## Still To Do
- **Desktop Hyprland install** — next up (GRUB now fully sorted)
- ~~**Disable Fast Boot in BIOS**~~ — DONE ✓ (03/04/2026)
- **Archive claude-memory repo** — both machines confirmed on vault now
- **Voice assistant** — build after desktop is set up
- **Hypridle** — screen dim/lock/suspend timers not configured on laptop
- **Gaps & borders** — window spacing/border thickness on laptop
- **Plymouth boot animation** — save for desktop
- **Gym Tracker Phase 2** — storage.py (save/load JSON)

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
