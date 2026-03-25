# Global Claude Instructions

## Session Start — Always do this first, in order

1. Detect the OS by running: `uname 2>/dev/null || echo "windows"`
2. Set the memory path based on the result:
   - If Linux → `/home/Lakira/Desktop/stuff/MyVault/Claude Memory`
   - If Windows → `C:\Users\lakir\Desktop\stuff\MyVault\Claude Memory`
3. Pull the latest memory from the vault repo:
   - Linux: `git -C /home/Lakira/Desktop/stuff/MyVault pull`
   - Windows: `git -C "C:\Users\lakir\Desktop\stuff\MyVault" pull`
4. Copy CLAUDE.md from the memory folder to the correct location:
   - Linux: `cp "/home/Lakira/Desktop/stuff/MyVault/Claude Memory/CLAUDE.md" /home/Lakira/.claude/CLAUDE.md`
   - Windows: `copy "C:\Users\lakir\Desktop\stuff\MyVault\Claude Memory\CLAUDE.md" "C:\Users\lakir\.claude\CLAUDE.md"`
5. Read these three files in full before doing or saying anything else:
   - `<memory_path>/lessons.md`
   - `<memory_path>/primer.md`
   - `<memory_path>/session-log.md`

## Session End — Always do this last

1. Rewrite `primer.md` with the current project status, what was completed, what's in progress, and what's next.
2. Append a new entry to `session-log.md` with the date, a summary of what was done, and any decisions made.
3. Copy the current CLAUDE.md into the memory folder:
   - Linux: `cp /home/Lakira/.claude/CLAUDE.md "/home/Lakira/Desktop/stuff/MyVault/Claude Memory/CLAUDE.md"`
   - Windows: `copy "C:\Users\lakir\.claude\CLAUDE.md" "C:\Users\lakir\Desktop\stuff\MyVault\Claude Memory\CLAUDE.md"`
4. Commit and push all changes via the vault repo:
   - Linux: `git -C /home/Lakira/Desktop/stuff/MyVault add . && git -C /home/Lakira/Desktop/stuff/MyVault commit -m "Session checkpoint" && git -C /home/Lakira/Desktop/stuff/MyVault push`
   - Windows: `git -C "C:\Users\lakir\Desktop\stuff\MyVault" add . && git -C "C:\Users\lakir\Desktop\stuff\MyVault" commit -m "Session checkpoint" && git -C "C:\Users\lakir\Desktop\stuff\MyVault" push`

## GitHub — Every Project
At the start of every session, check if the current project directory has a GitHub remote set up:
```
gh repo view 2>/dev/null
```
If no remote exists:
1. Run `gh repo create <project-name> --private --source=. --remote=origin --push` to create a private repo and push
2. If the directory isn't a git repo yet, run `git init` and `git add .` and `git commit -m "Initial commit"` first

Default visibility: **private** unless the user says otherwise.

## Memory Files
| File | Purpose |
|---|---|
| `lessons.md` | User preferences, communication style, corrections — apply these always |
| `primer.md` | Current project status, what's next, what's blocked |
| `session-log.md` | Running log of all sessions and changes |
