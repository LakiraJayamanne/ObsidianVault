---
tags:
  - spid
  - homelab
  - advice
links:
  - "[[Homelab & JARVIS Architecture]]"
date: 2026-05-15
source: Ismail (WhatsApp)
---

# Advice — Ismail (homelab, 15/05/2026)

Context: Lakira mentioned getting SPID (JARVIS) running on a Pi 5. Ismail runs a serious home server and gave advice.

---

## Ismail's hardware (for reference)
- Dual Xeon 6248s
- 256GB ECC DDR4 @ 3200 MT/s
- Titan X Pascal + GTX 780
- 4x 10TB HDD in RAID Z1 with 3x 1TB SSD cache
- 8x 4TB SAS SSDs in RAID Z2
- 2x 25Gb SFP ports

---

## Claude API cost warning
- Used Sonnet for 10 minutes → £2 spent
- At real working-session usage (long context, multiple sessions/day), Claude API = £25-35/month
- **Recommendation: use Ollama for cloud models** — NVIDIA Nemotron available free via NVIDIA NIM
- Groq (Llama 3.3 70B) also free and OpenAI-compatible — fast enough for voice

---

## Advice for SPID on Pi 5

### Pi 5 is fine
- He ran OpenClaw on a Pi 4 4GB — said "you'll be fine lol"
- Pi 5 is significantly faster than Pi 4 — SPID's Docker stack (Pi-hole, Jellyfin, Nextcloud, voice layer) is well within reach
- People run Kubernetes and full Docker stacks on Pi's routinely

### Jellyfin / media
- He ran Plex and Jellyfin on a 5th gen i7 with 16GB RAM
- For DLNA purposes and playing movies, even without Jellyfin app it works fine
- 1080p streaming plan confirmed viable

### ⚠️ Set a static IP — important
- "Even the Ethernet port on the mobo will be fine. If you can't wire it into the router then make sure you can set a static IP for it on your network rather than DHCP"
- **Why this matters for SPID:**
  - iPhone Shortcuts call the Pi by IP — if DHCP reassigns it, Shortcuts break
  - Desktop SSH (for VRAM check via rocm-smi) uses the Pi's IP — breaks on reassignment
  - Any local DNS entries or Pi-hole config referencing the IP breaks
- **How to do it:** Either set static IP on the Pi itself (`/etc/dhcpcd.conf` or NetworkManager) OR set a DHCP reservation in the router (preferred — router always hands out the same IP to the Pi's MAC address)
