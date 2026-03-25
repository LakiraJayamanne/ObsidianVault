# Project Primer

## Current Status
Hyprland on Fedora — **Fully working. SDDM fixed. ✓**
- SDDM fix confirmed: `DisplayServer=x11` in `/etc/sddm.conf.d/kde_settings.conf` — root cause was SDDM defaulting to Wayland greeter
- Real config at `~/.config/hypr/`, waybar/swww/swaync running via exec-once
Gym Tracker — Phase 1 complete. Ready to start Phase 2 (`storage.py`).
Memory system — **migrated to Obsidian vault** (`MyVault/Claude Memory/`). Auto-commits via Stop hook. ✓

## In Progress
- **CO1106 Cinema Ticket Coursework** — wireframes done and pushed to GitLab ✓
- **Desktop rice plan** — decided to port laptop dotfiles directly (not clone caelestia), use caelestia as visual reference only. Do this after vacation (~31 Mar).

## Completed This Session (Session 36)
- CO1106 wireframes confirmed pushed to GitLab (done before this session)
- Installed ghgrab (cargo install ghgrab) — TUI tool for downloading specific files/folders from GitHub repos
- Fixed ghgrab PATH issue: fish_add_path ~/.cargo/bin
- Note: use ghgrab whenever grabbing files from a GitHub repo instead of cloning the whole thing

## Completed This Session (Session 33)
- Fixed Nautilus Super+E — changed to `nautilus --new-window` so it always opens fresh
- CO1109 exam revision notes created in vault (Lecture Notes/CO1109/Exam Revision — CO1109.md) — all 9 lectures, formulas, compare/contrast tables, cheat sheet
- Desktop dual boot plan noted — Bazzite + Hyprland, after vacation, RX 6700XT, partition carefully around games
- Installed lazygit (binary to ~/.local/bin) — git TUI, taught basic usage
- Built ghgraph script (~/.local/bin/ghgraph) — GitHub contribution graph in terminal, GitHub green palette, month labels
- Discussed Bazzite as gaming distro (Fedora-based), decided single Bazzite+Hyprland install beats dual Linux boot
- Skipped leg day (23 Mar) — continuing plan: rest Monday, Push Tuesday

## Completed This Session (Session 32)
- CO1106 Week 10 wireframes done in Figma — Page 1 (movie search) + Page 2 (search results). Exported as PNG, added to group61 repo. Weeklylog.md updated with Week 10 end of week entry. Waiting on Alpha before pushing.
- Ender Magnolia working via Wine — fixed with vcrun2022 via winetricks. Desktop file created at ~/.local/share/applications/ender-magnolia.desktop.

## Completed This Session (Session 31)
- Game recommendations for 4-day countryside vacation (27 Mar): Oxenfree + Undertale
- Installed Lutris (Flatpak 0.5.22), connected Epic Games library (145 games imported)
- Set up Wine-GE runner in Lutris
- Installed qt6ct, set Qt apps to dark theme, added QT_QPA_PLATFORMTHEME=qt6ct to fish + hyprland env
- Super+E changed from yazi to Nautilus
- Undertale (jc141 Linux native): working via launch.sh + desktop file in rofi. Fixed fuse-overlayfs missing dependency.
- Death's Door (FitGirl): installed and ran but ~20-30fps on 760M through Wine — uninstalled
- Ender Magnolia: downloading FitGirl repack — 2D Metroidvania, should run well
- Oxenfree: Windows build via Wine — black screen, never resolved. jc141 native has 1 seeder (too slow)
- Dynamic folder colors: papirus-dynamic.sh script created, hooked into both wallpaper scripts
- Nautilus opacity set to 0.8 in Hyprland rules

## Game Setup Notes
- Undertale launch: `bash /home/Lakira/Games/Undertale/launch.sh` (needs DISPLAY=:0, fuse-overlayfs)
- Desktop files created for: Undertale, Oxenfree (in ~/.local/share/applications/)
- Wine+DXVK working: use `DISPLAY=:0 WINEDLLOVERRIDES="d3d11,dxgi=n" wine game.exe`
- jc141 Linux native builds: need fuse-overlayfs, run start.n.sh from within game directory
- FitGirl repacks: run setup.exe with `DISPLAY=:0 wine setup.exe`, install to ~/Games/

## Already Working (don't redo)
- `Super+Q` → Persona Quickshell blade menu (POWER/STATS/CLAUDE) — running via exec-once
- `Super+W` → wallpaper picker (wppicker.sh)
- `Super+Shift+W` → cycle wallpaper
- `Super+Ctrl+B` → waybar style switcher
- `Super+Alt+B` → waybar layout switcher
- `Super+L` → hyprlock
- `Super+E` → Nautilus
- Power button left-click → wlogout
- `Super+D` → rofi app launcher
- `Super+Tab` → rofi window switcher
- Fish opens on every terminal with spidey oh-my-posh prompt + fastfetch on startup
- hyprpolkitagent running
- Waybar wallpaper widget: left click cycles, right click opens picker
- Bibata-Modern-Ice cursor active
- Dynamic theming via matugen (wallpaper → colors → waybar, kitty, rofi, hyprlock, wlogout, btop, gtk, cava)
- Dynamic papirus folder colors via papirus-dynamic.sh (hooked into wallpaper scripts)

## After Vacation — Quickshell
- **Persona Quickshell full install** — all assets in repo (videos, PNGs, QML). Decided to wait until after vacation. Repo: https://github.com/Yujonpradhananga/Persona-Quickshell-
- Current simplified version works (POWER/STATS/CLAUDE blades, Super+Q). Full repo has: :3 button, spring animations, P3R power menu with video, music player, app carousel.

## Still To Do / Consider
- **Hypridle** — screen dim/lock/suspend timers not configured at all
- **SDDM** — ✓ working (DisplayServer=x11 fix, SilentSDDM theme active)
- **Gaps & borders** — user says current spacing is fine, skip for now
- **Plymouth boot animation** — custom frame-sequence animation
- **Gym Tracker Phase 2** — `storage.py` (save/load JSON)
- **Oxenfree** — still not working, needs jc141 native torrent with more seeds or different approach
- **Desktop dual boot (Fedora)** — plan after vacation (back ~31 Mar). GPU is RX 6700XT (AMDGPU, no driver issues). Need to partition carefully around 215GB games/Steam library. Goal: Hyprland + caelestia-inspired rice, adapting existing laptop dotfiles. Do partition planning first session back.

## Desktop Only
- **Guide Tracker app** — project for Lakira's dad, only on the Windows desktop.

## Gym Tracker Build Phases
1. [x] Phase 1 — Data structures (ExerciseSet, Session, Log classes) → `models.py`
2. [ ] Phase 2 — Storage (save/load JSON) → `storage.py`
3. [ ] Phase 3 — Text menu → `main.py`
4. [ ] Phase 4 — Algorithms (overload, plateau, bodyweight trend) → `algorithms.py`
5. [ ] Phase 5 — Polish

## Gym Data Logged So Far
- Session 1: Pull Day — 17/03/2026 — BW 71kg
- Session 2: Push Day — 20/03/2026 — BW 72kg (clothes, no shoes)

## Vacation (27 Mar 2026)
- 4 days, countryside, no mouse, laptop only
- Games planned: Undertale (working), Ender Magnolia (downloading)
- New Yeat album also drops 27th March

## After Vacation — 1 Month Off (from ~31 Mar 2026)
- Full month off uni — good time for big projects
- **Priority: Desktop dual boot** — Bazzite (Fedora-based) + Hyprland, caelestia-inspired rice on the big screen with RX 6700XT
- Gym Tracker Phase 2 + 3
- Anything else that's been sitting on the backlog
