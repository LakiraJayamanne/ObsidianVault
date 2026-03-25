---
name: Gym logging reminder
description: When Lakira goes to the gym, set a reminder for when he gets back to log his workout in the Gym Tracker
type: feedback
---

When Lakira mentions he's going to the gym, set a one-shot reminder for his estimated return time to log his workout in the Gym Tracker.

**Why:** He asked for this explicitly — wants to be prompted to log sessions rather than forget.

**How to apply:** Use CronCreate with recurring: false. Remind him: "Hey, you're back from the gym — don't forget to log your workout in the Gym Tracker!" Note that reminders are session-only, so warn him to keep the session open.
