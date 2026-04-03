---
tags:
  - desktop
  - fedora
  - grub
  - setup
---

# GRUB Setup — Desktop (Fedora 43)

**Theme:** Valhalla (from [[Gorgeous-GRUB]])
**Resolution:** 1920x1080 (no font adjustment needed)
**Entries:** `Fedora` + `Windows 11`
**Timeout:** 5 seconds

---

## Step 1 — Install Valhalla Theme

```bash
git clone https://github.com/happyzxzxz/valhallaDots
cd valhallaDots
chmod +x install.sh
./install.sh
```

When prompted, choose GRUB theme. Files go to `/boot/grub2/themes/`.

---

## Step 2 — Edit /etc/default/grub

```bash
sudo nano /etc/default/grub
```

Set/change these lines:
```
GRUB_DISTRIBUTOR="Fedora"
GRUB_TIMEOUT=5
GRUB_DISABLE_OS_PROBER=true
```

---

## Step 3 — Get Windows UUID

```bash
sudo blkid | grep ntfs
```

Copy the UUID for your Windows partition (nvme0n1p3).

---

## Step 4 — Add Manual Windows Entry

```bash
sudo nano /etc/grub.d/40_custom
```

Add at the bottom (replace `YOUR-UUID-HERE` with the UUID from step 3):
```
menuentry "Windows 11" {
    search --fs-uuid --no-floppy --set=root YOUR-UUID-HERE
    chainloader /EFI/Microsoft/Boot/bootmgfw.efi
}
```

---

## Step 5 — Rebuild GRUB

```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

Reboot. Done.
