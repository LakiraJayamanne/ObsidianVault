---
name: obsidian-vault-checkpoint
description: Always commit and push the Obsidian vault when saving a checkpoint
type: feedback
---

Always commit and push the Obsidian vault at /home/Lakira/Desktop/stuff/MyVault when saving a checkpoint.

**Why:** User wants vault changes synced to GitHub whenever memory is saved.

**How to apply:** After committing memory files, also run `git add . && git commit -m "vault backup: $(date '+%Y-%m-%d %H:%M:%S')" && git push` from the vault directory.
