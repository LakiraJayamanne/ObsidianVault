---
tags:
  - claude-memory
  - claude/status
---

# Project Primer

Current project status, what's in progress, what's next.

---

## Current Status
- **Hyprland on Fedora** — Fully working. SDDM fixed. ✓
- **Gym Tracker** — Phase 1 complete. Ready to start Phase 2 (storage.py).
- **Memory system** — Migrating from claude-memory repo → Obsidian vault (in progress)
- **Obsidian vault** — Cleaned up, synced to GitHub ✓

## In Progress
- **Memory migration** — Moving all memory into Obsidian vault (z Meta/Claude/)
- **Desktop rice plan** — Saving all GPU-heavy Quickshell stuff for desktop dual boot
- **Voice for Claude** — Discussed, not started. Leaning towards edge-tts or ElevenLabs. Against OpenAI TTS.

## After Vacation (from ~31 Mar 2026)
- Full month off uni — good time for big projects
- **Priority: Desktop dual boot** — Fedora + Hyprland, full Persona Quickshell rice on RX 6700XT
- Gym Tracker Phase 2 + 3
- Voice for Claude

## Still To Do
- **Hypridle** — screen dim/lock/suspend timers not configured
- **Gaps & borders** — window spacing, border thickness
- **Plymouth boot animation** — custom frame-sequence animation (desktop only)
- **Desktop dual boot (Fedora)** — RX 6700XT, need to partition around 215GB games library
- **Laptop vault migration** — move from Desktop/stuff/MyVault to Documents/Obsidian/MyVault

## Already Working (don't redo)
- Super+Q → Persona Quickshell blade menu (POWER/STATS/CLAUDE)
- Super+W → wallpaper picker
- Super+Shift+W → cycle wallpaper
- Super+Ctrl+B → waybar style switcher
- Super+Alt+B → waybar layout switcher
- Super+L → hyprlock
- Super+E → Nautilus
- Power button left-click → wlogout
- Super+D → rofi app launcher
- Super+Tab → rofi window switcher
- Fish + spidey oh-my-posh prompt + fastfetch on startup
- Dynamic theming via matugen (wallpaper → colors → everything)
- Dynamic papirus folder colors via papirus-dynamic.sh
- Bibata-Modern-Ice cursor active

## Gym Tracker Build Phases
1. [x] Phase 1 — Data structures (ExerciseSet, Session, Log) → models.py
2. [ ] Phase 2 — Storage (save/load JSON) → storage.py
3. [ ] Phase 3 — Text menu → main.py
4. [ ] Phase 4 — Algorithms (overload, plateau, bodyweight trend) → algorithms.py
5. [ ] Phase 5 — Polish

## Gym Data Logged So Far
- Session 1: Pull Day — 17/03/2026 — BW 71kg
- Session 2: Push Day — 20/03/2026 — BW 72kg (clothes, no shoes)
