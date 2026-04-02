---
tags:
  - claude-memory
  - claude/projects
---

# Projects

## Gym Tracker
Python CLI workout tracker.
- **Windows:** `C:\Users\lakir\Documents\Projects\gym-tracker`
- **Linux:** `/home/Lakira/Documents/PROGRAMMING/PERSONAL/Gym Tracker/`
- **GitHub:** github.com/LakiraJayamanne/gym-tracker
- Full context in `CONTEXT.md` inside the project directory — always read it at session start

**Goal:** Track gym progress, get progressive overload suggestions, monitor bodyweight while cutting for summer.

Phases:
1. [x] models.py — ExerciseSet, Session, Log classes
2. [ ] storage.py — save/load JSON
3. [ ] main.py — text menu
4. [ ] algorithms.py — overload, plateau, bodyweight trend
5. [ ] Polish

---

## Guide Tracker
App for Lakira's dad. Desktop (Windows) only.
- Flask backend (app.py, models.py, database.py, checkins.py, geofence.py)
- Frontend (index.html)
- GitHub: GuideTracker (public)

---

## CO1106 Cinema Coursework
Group project — cinema ticket booking/comparison web app.
- **Repo:** `C:\Users\lakir\Documents\Projects\group61`
- **GitLab:** git@git1.mcs.le.ac.uk:2026-co1106/group61.git
- Team: Isabela, Lakira, Callum, Alpha, Yaser (inactive)
- Lakira's tasks assigned per week in Weeklylog.md

---

## Plymouth Boot Animation
Custom boot animation using frame sequences from a video.
- Not started — save for desktop dual boot
- Plan: ffmpeg to extract frames → Plymouth script theme → set active via `plymouth-set-default-theme`

---

## Desktop Dual Boot (Fedora) — DONE ✓ (02/04/2026)
Drive: KINGSTON SNV2S1000G 1TB NVMe (nvme0n1)
- p1: EFI System 105MB (shared with Windows)
- p3: Windows NTFS 850GB (shrunk from 999GB)
- p5: Fedora swap 2.15GB
- p6: Fedora Btrfs 147GB (/ and /home subvolumes)
- NTFS resize fix: chkdsk /f /r → ntfsfix -d → ntfsresize --force → parted resizepart
- Post-install Windows BSOD fixed with ntfsfix from live USB

## Desktop Rice Plan (Fedora — save for RX 6700XT sessions)
Setup order:
1. Fedora dual boot + Hyprland base ← next
2. claw-code + Ollama (Claude Code cooldown fallback, set up BEFORE ricing)
3. Caelestia as the base shell (Material You, fish-native, good Qt/GTK)
4. Port ilyamiro widgets into caelestia: music EQ popup, DDG wallpaper search, focus time tracker
5. Plymouth boot animation (80-frame sequence, reference ilyamiro's repo)

Repos cloned at `~/quickshell/persona-qs/` (Persona Quickshell)
Upgrade plan at `~/Desktop/quickshell_upgrade_plan.md`

### ilyamiro/nixos-configuration — Key Patterns Worth Stealing
- **Morphing master window**: single FloatingWindow `qs-master` at -5000,-5000, teleports + resizes + StackView swaps for all popups
- **MatugenColors.qml**: polls `/tmp/qs_colors.json` every 1s for live color updates across all widgets
- **IPC**: `qs_manager.sh` writes to `/tmp/qs_widget_state`, Main.qml polls every 50ms
- **Focus time daemon**: Python + SQLite, tracks per-app active window time
- **DDG wallpaper search**: integrated into picker, streams results live via `get_ddg_links.py`
- **Workspace pills**: staggered startup animation (each pill delays index×60ms)
- **Lock screen**: custom QML using `Quickshell.Services.Pam` — not hyprlock
- **Plymouth**: 80-frame animation + separate 80-frame progress sequence (PNGs included in repo)

---

## Memory Sync Test
Secret phrase: *"the rain in spain falls mainly on the plane"*
Used to verify memory syncs between laptop and desktop.
