---
tags:
  - gaming
  - minecraft
---

# Minecraft Server Plan

**Loader:** Fabric
**MC Version:** 1.21.1
**Hosting:** Oracle Cloud Free Tier (ARM, 4 core, 24GB RAM)
**Players:** 6-8 friends, occasional sessions

---

## SERVER MODS

### Performance
- Fabric API
- Lithium
- Krypton
- FerriteCore
- C2ME
- ModernFix
- Very Many Players (VMP)
- Noisium

### World Generation
- Terralith
- Tectonic
- Incendium (Nether overhaul)
- Deeper and Darker (new dimension)
- Regions Unexplored
- Chunky *(run once on world creation to pre-gen chunks)*

### Content
- Naturalist (wildlife mobs)
- Farmer's Delight Refabricated
- Explorify
- Origins
- Vein Mining
- Carry On
- Sophisticated Backpacks
- Wearable Lanterns
- Right Click Harvest
- Towns and Towers
- Repurposed Structures

### YUNG's Structure Suite
- YUNG's API *(required)*
- YUNG's Better Dungeons
- YUNG's Better Mineshafts
- YUNG's Better Strongholds
- YUNG's Better Ocean Monuments
- YUNG's Better Witch Huts
- YUNG's Better Desert Temples
- YUNG's Better Jungle Temples
- YUNG's Better Nether Fortresses
- YUNG's Bridges
- YUNG's Extras

### Multiplayer QoL
- Simple Voice Chat
- Waystones
- Universal Graves
- Skin Overrides

### Admin / Monitoring
- Spark
- Carpet
- Ledger
- TabTPS
- Bluemap

---

## CLIENT MODS

> All "both" mods above also need to be installed client-side. List below is client-only additions.

### Performance
- Sodium
- Iris
- ImmediatelyFast
- FerriteCore
- Entity Culling
- Cull Fewer Leaves
- ModernFix
- Dynamic FPS

### Visual
- Voxy
- Euphoria Patches
- Better Clouds
- Particle Rain
- Dense Flowers
- Cozy Critters
- Continuity
- Camera Overhaul
- Wakes
- LambDynamicLights
- 3D Skin Layers
- Not Enough Animations
- Eating Animation
- Blur+

### Audio
- Atmosfera
- Presence Footsteps
- Sounds (Extra Sounds Updated)
- Immersive Music
- Sound Physics Remastered

### Particles / Effects
- Inventory Particles
- Footprint Particle
- Immersive Hotbar
- Hold My Items
- Subtle Effects
- Particle Interactions
- Visuality
- Swinging Lanterns
- Tidy Fire

### QoL
- Mod Menu
- Better F3
- Zoomify
- Mouse Tweaks
- Fast Quit
- Auto HUD
- Make Bubbles Pop
- Xaero's Minimap
- Xaero's World Map
- REI (Roughly Enough Items)
- Jade
- AppleSkin
- Inventory Profiles Next
- Sodium Extra
- Reese's Sodium Options
- MiniHUD
- Resourcify

### Third Person
- Smooth Third Person Camera
- Shoulder Surfing Reloaded

---

## RESOURCE PACKS (client, optional)
- Complementary Reimagined *(shader)*
- Fresh Animations
- Fresh Animations Player Extension
- Fresh Animations Extensions *(Naturalist mob compat)*
- Theon's Eating Animation Pack
- Rainbow's Foliage *(needs Polytone mod)*
- O's Colorful Grasses
- Mickey Joe's Flowers
- Bushy Pink Petals
- Fancy Crops
- Torches Reimagined
- Extended Illuminate
- Fire Rekindled
- Zombie Overhaul

---

## ORACLE CLOUD SETUP

### 1. Create account
- cloud.oracle.com — use real card for verification, won't be charged
- If rejected during signup, try different browser

### 2. Create instance
- Compute → Instances → Create Instance
- Shape: VM.Standard.A1.Flex (Ampere)
- OCPUs: 4, RAM: 24GB
- OS: Ubuntu 22.04
- Generate SSH key pair, download private key

### 3. Open firewall ports
**Oracle side:** Instance → Subnet → Security List → Add Ingress Rules
| Port | Protocol | Purpose |
|---|---|---|
| 25565 | TCP | Minecraft |
| 24454 | UDP | Voice Chat |
| 8100 | TCP | Bluemap |

**Ubuntu side (after SSH in):**
```bash
sudo iptables -I INPUT -p tcp --dport 25565 -j ACCEPT
sudo iptables -I INPUT -p udp --dport 24454 -j ACCEPT
sudo iptables -I INPUT -p tcp --dport 8100 -j ACCEPT
sudo netfilter-persistent save
```

### 4. SSH in
```bash
ssh -i ~/path/to/key.key ubuntu@YOUR_IP
```

### 5. Install Java 21
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y openjdk-21-jre-headless
```

### 6. Set up server
```bash
mkdir ~/minecraft && cd ~/minecraft
# Upload fabric-server-launch.jar from fabricmc.net
java -jar fabric-server-launch.jar --installMCVersion 1.21.1 --downloadMinecraft
echo "eula=true" > eula.txt
```

### 7. Start script
```bash
nano start.sh
```
```bash
#!/bin/bash
java -Xms8G -Xmx16G -jar fabric-server-launch.jar nogui
```
```bash
chmod +x start.sh
```

### 8. Upload mods
```bash
# From local machine:
scp -i ~/key.key *.jar ubuntu@YOUR_IP:~/minecraft/mods/
```

### 9. Pre-generate chunks (run once after first start)
In server console:
```
chunky center 0 0
chunky radius 5000
chunky start
```

### 10. Run as service
```bash
sudo nano /etc/systemd/system/minecraft.service
```
```
[Unit]
Description=Minecraft Server
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/minecraft
ExecStart=/home/ubuntu/minecraft/start.sh
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
```bash
sudo systemctl enable minecraft
sudo systemctl start minecraft
```

### Done
Give friends the Oracle instance IP. Op yourself in console: `/op YourUsername`

---

## NOTES
- Shaders are client-side — everyone installs what they want
- Voxy, DH, all visual mods are client-side only
- Waystones XP cost — configure in config if you want them free
- Origins — everyone picks on first join, can't change without a command
- Set a world border to limit chunk generation beyond Chunky pre-gen area
- Mods dropped: Alex's Mobs (Forge only 1.21.x), Spelunkery (dead mod)
