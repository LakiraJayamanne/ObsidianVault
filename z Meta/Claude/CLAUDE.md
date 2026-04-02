# Global Claude Instructions

## Session Start — Always do this first, in order

1. Detect the OS by running: `uname 2>/dev/null || echo "windows"`
2. Detect which machine you're on:
   - Linux: run `lspci | grep -i vga` — if output contains "Radeon RX 6700" → **desktop**. If it contains "Radeon 760M" or "HawkPoint" → **laptop**.
   - Windows: run `wmic path win32_VideoController get name` — same logic applies.
   - Hold this for use in greetings and advice (e.g. don't recommend Whisper on laptop, don't suggest laptop-only keybinds on desktop).
3. Set the vault path based on the result:
   - If Linux → `$HOME/Documents/Obsidian/MyVault`
   - If Windows → `C:\Users\lakir\Documents\Obsidian\MyVault`
4. Pull the latest vault from GitHub:
   - Linux: `git -C "$HOME/Documents/Obsidian/MyVault" pull`
   - Windows: `git -C "C:\Users\lakir\Documents\Obsidian\MyVault" pull`
5. Read these files in full before doing or saying anything else:
   - `<vault_path>/z Meta/Claude/lessons.md`
   - `<vault_path>/z Meta/Claude/primer.md`
   - `<vault_path>/z Meta/Claude/session-log.md` (last 50 lines only)

## Session End — Always do this last

1. Rewrite `z Meta/Claude/primer.md` with current project status, what was completed, what's in progress, what's next.
2. Append a new entry to `z Meta/Claude/session-log.md` with the date, summary of what was done, and any decisions made.
3. Commit and push all vault changes to GitHub:
   - Linux: `git -C "$HOME/Documents/Obsidian/MyVault" add . && git -C "$HOME/Documents/Obsidian/MyVault" commit -m "Session checkpoint" && git -C "$HOME/Documents/Obsidian/MyVault" push`
   - Windows: `git -C "C:\Users\lakir\Documents\Obsidian\MyVault" add . && git -C "C:\Users\lakir\Documents\Obsidian\MyVault" commit -m "Session checkpoint" && git -C "C:\Users\lakir\Documents\Obsidian\MyVault" push`

## GitHub — Every Project
At the start of every session, check if the current project directory has a GitHub remote set up:
```
gh repo view 2>/dev/null
```
If no remote exists:
1. Run `gh repo create <project-name> --private --source=. --remote=origin --push` to create a private repo and push
2. If the directory isn't a git repo yet, run `git init` and `git add .` and `git commit -m "Initial commit"` first

## Memory Files (in vault at z Meta/Claude/)
| File | Purpose |
|---|---|
| `lessons.md` | Preferences, communication style, corrections — apply always |
| `primer.md` | Current project status, what's next, what's blocked |
| `session-log.md` | Running log of all sessions and changes |
| `about-lakira.md` | Personal facts, interests, identity |
| `tech-setup.md` | Machines, OS, tools, accounts, paths |
| `projects.md` | All active projects and their status |
