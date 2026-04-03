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
- **Desktop GRUB** — Partially working. Theme disabled (Valhalla was causing black screen). Console mode active. menu_auto_hide unset. Windows 11 entry present. ⚠️
- **Desktop Windows boot fix** — CONFIRMED WORKING ✓ (03/04/2026)
- **Desktop Hyprland install** — DONE ✓ (03/04/2026)
- **Desktop boot hang** — FIXED ✓ (03/04/2026) — Root cause: Valhalla GRUB theme silently black-screened. Fixed by disabling theme + forcing console mode.
- **Desktop Hyprland** — Booting but config broken due to Hyprland 0.51.1 update. rgba syntax errors (186+). No keybinds/bar. In progress. ⚠️
- **Monitor @ 165Hz** — Set in /home/lakira/.config/hypr/hyprland/monitors/default.conf ✓
- **Zen Browser** — Installed via Flatpak, profile synced from laptop ✓
- **Spicetify** — Installed, prefs_path set manually, backup applied ✓ (needs flatpak chmod fix to complete)
- **Wallpapers** — Synced from laptop to ~/Pictures/Wallpapers ✓
- **System dark mode** — Set via gsettings ✓
- **Caelestia rice** — Installed via caelestia-fedora fork (EnceladusII/caelestia-fedora) ✓ (03/04/2026)
  - Frozen at August 2025 snapshot of upstream caelestia
  - Can update shell via: cd ~/.config/quickshell/caelestia && git pull (risk: Quickshell version mismatch)
  - Hyprland config backed up to ~/hypr-backup before install
  - Config now split across ~/.config/hypr/hyprland/*.conf
  - Monitor conf at ~/.config/hypr/hyprland/monitors/default.conf
- **Gym Tracker** — Phase 1 complete. Ready to start Phase 2 (storage.py).
- **Memory system** — Fully migrated to Obsidian vault (z Meta/Claude/). ✓
- **Obsidian vault** — Main base for Claude memory. Synced to GitHub (ObsidianVault repo). ✓
- **Voice Assistant** — Stack decided. Not started. Waiting on desktop rice.

## Memory System — How It Works
- All memory lives in the vault at `z Meta/Claude/`
- Claude reads `lessons.md`, `primer.md`, `session-log.md` at session start
- Claude writes/commits/pushes the ObsidianVault repo at session end
- Obsidian Git plugin removed — Claude handles git
- Old `claude-memory` repo to be archived (both machines now confirmed on vault)

## In Progress
- **Desktop Hyprland config — BROKEN** — Hyprland updated to 0.51.1 during caelestia install, breaking rgba color syntax. 186+ errors. No keybinds (except Super+T=terminal), no bar.
  - Fix: update rgba() values in ~/.config/hypr/hyprland/decoration.conf and others to 0.51.1 syntax
  - Config split across: env, general, input, misc, animations, decoration, group, execs, rules, keybinds + hypr-user.conf
  - Super+T opens kitty ✓

## GRUB State (desktop) — needs cleanup
- Theme: DISABLED (Valhalla was causing silent black screen on boot)
- GRUB_TERMINAL_OUTPUT=console (added to fix visibility)
- GRUB_CMDLINE_LINUX="nomodeset" (added for debugging — remove once stable)
- To restore: remove nomodeset, re-enable gfxterm, find a working theme (NOT Valhalla)
- menu_auto_hide unset from grubenv ✓
- Two kernels present: 6.17.1-300.fc43 and 6.19.10-200.fc43. Default set to 6.17.1.

## Priority Order
1. **Fix Hyprland 0.51.1 config** ← next (on desktop, rgba syntax + keybinds + bar) 
2. **Finish Spicetify setup** — still needs flatpak chmod + apply to complete
3. **Desktop rice** — caelestia customisation + ilyamiro widgets
4. **Clean up GRUB** — remove nomodeset, restore graphical theme
5. **claw-code + Ollama** — set up as Claude Code cooldown fallback
6. **Voice assistant** — build starts after above

## GRUB Notes (desktop)
- Theme: Valhalla installed to /boot/grub2/themes/valhalla/ but DISABLED — was causing silent black screen on every boot
- GRUB_TERMINAL_OUTPUT=console — forced text mode to fix boot visibility
- GRUB_CMDLINE_LINUX="nomodeset" — added for debugging, remove when done
- Fast Boot disabled in BIOS ✓ (03/04/2026)
- menu_auto_hide unset from grubenv — keeps getting reset by kernel updates, may need to re-unset after dnf updates

## Caelestia Notes (desktop)
- Installed via EnceladusII/caelestia-fedora (abandoned Fedora fork, frozen Aug 2025)
- Quickshell installed via COPR (errornointernet/quickshell)
- Shell lives at ~/.config/quickshell/caelestia
- Hyprland config restructured — now sources from ~/.config/hypr/hyprland/*.conf
- User overrides go in ~/.config/caelestia/hypr-vars.conf and hypr-user.conf
- Keybinds at ~/.config/hypr/hyprland/keybinds.conf (need to verify laptop keybinds ported correctly)
- Bar is on the left (default) — can move to top via shell.json if desired

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
- **Fix Hyprland 0.51.1 rgba config errors** — in progress on desktop
- **Finish Spicetify** — chmod flatpak dir + re-run backup apply
- **Archive claude-memory repo** — both machines confirmed on vault now
- **Voice assistant** — build after desktop is set up
- **Hypridle** — screen dim/lock/suspend timers not configured on laptop
- **Gaps & borders** — window spacing/border thickness on laptop
- **Plymouth boot animation** — save for desktop
- **Gym Tracker Phase 2** — storage.py (save/load JSON)
- **claw-code + Ollama** — desktop setup

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
