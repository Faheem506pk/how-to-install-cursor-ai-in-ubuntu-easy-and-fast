Here's your full installation guide in `README.md` format:

---

````markdown
# 🖥️ Install Cursor AI (.AppImage) on Ubuntu

## ✅ Prerequisites
- Ubuntu installed
- `.AppImage` file for Cursor AI downloaded

---

## 📥 Step 1: Download Cursor AI AppImage

Download the `.AppImage` file and rename it to:

```bash
cursor.appimage
````

---

## 📁 Step 2: Make it executable

```bash
cd ~/Downloads
chmod a+x cursor.appimage
```

---

## 📦 Step 3: Install `libfuse2`

```bash
sudo apt install libfuse2
```

---

## 🚚 Step 4: Move AppImage to `/opt`

```bash
sudo mv cursor.appimage /opt/cursor.appimage
```

---

## 🖼️ Step 5: Create a Desktop Entry

```bash
sudo nano /usr/share/applications/cursor.desktop
```

Paste the following (change `[username]` to your actual username, e.g., `faheem506pk`):

```ini
[Desktop Entry]
Name=Cursor AI IDE
Exec=/opt/cursor.appimage
Icon=/home/faheem506pk/.local/share/icons/cursor.png
Type=Application
Categories=Development;
```

> Save: `Ctrl + O`, then `Enter`, then `Ctrl + X`

---

## 🖱️ Step 6: Create a CLI Command

```bash
sudo nano /usr/local/bin/cursor
```

Paste:

```bash
#!/bin/bash
/opt/cursor.appimage "$@" > /dev/null 2>&1 &
```

> Save: `Ctrl + O`, then `Enter`, then `Ctrl + X`

Make it executable:

```bash
sudo chmod +x /usr/local/bin/cursor
```

---

## 🔐 Step 7: AppArmor Permissions

```bash
sudo nano /etc/apparmor.d/cursor-appimage
```

Paste:

```apparmor
#include <tunables/global>

profile cursor /opt/cursor.AppImage flags=(unconfined) {
  #include <abstractions/base>

  /opt/cursor.AppImage mr,
  owner @{HOME}/** rw,
  /tmp/** rwk,
  /proc/sys/kernel/yama/ptrace_scope r,
  /sys/devices/system/cpu/cpufreq/policy*/cpuinfo_max_freq r,
}
```

> Save: `Ctrl + O`, then `Enter`, then `Ctrl + X`

Apply AppArmor profile:

```bash
sudo apparmor_parser -r /etc/apparmor.d/cursor-appimage
```

---

## ✅ Step 8: Launch Cursor AI

```bash
cursor
```

---

## ❓ Cursor Icon Not Showing?

Make sure the icon exists at this path:

```
/home/faheem506pk/.local/share/icons/cursor.png
```

If it doesn't display:

* Check if the image is a valid `.png`
* Verify permissions: `chmod 644 cursor.png`
* Reboot or run: `update-desktop-database`

---

Enjoy coding with Cursor AI! 🚀

```

--- 

Let me know if you want this as a downloadable `README.md` file too.
```
