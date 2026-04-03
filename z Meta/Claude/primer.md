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
- **Desktop Windows boot fix** — CONFIRMED WORKING ✓ (03/04/2026)
- **Desktop Hyprland install** — DONE ✓ (03/04/2026)
- **Desktop Hyprland first boot** — CONFIRMED WORKING ✓ (03/04/2026)
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
- **Caelestia first boot — BROKEN** — desktop hangs on black screen when booting Fedora. GRUB timeout too short to catch manually. Diagnosing via Fedora live USB chroot — about to do this next.
  - Symptom: ASUS logo stays up, then black screen. Never reaches SDDM.
  - Likely cause: kernel/initramfs hang or SDDM failing early in boot
  - Plan: boot live USB → chroot → fix GRUB timeout → check journalctl for hang cause

## Priority Order
1. **Fix desktop Fedora boot hang** ← next (live USB chroot)
2. **Finish Spicetify setup** — still needs flatpak chmod + apply to complete
3. **Desktop rice** — caelestia customisation + ilyamiro widgets
4. **claw-code + Ollama** — set up as Claude Code cooldown fallback
5. **Voice assistant** — build starts after above

## GRUB Notes (desktop)
- Theme: Valhalla — installed to /boot/grub2/themes/valhalla/
- GRUB_TERMINAL_OUTPUT="gfxterm" is commented out — if theme renders broken, uncomment and rebuild
- Fast Boot disabled in BIOS ✓ (03/04/2026) — GRUB now shows on warm reboot
- menu_auto_hide unset from grubenv — was silently skipping menu on cold boot

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
- **Fix desktop Fedora boot hang** — live USB chroot in progress
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
