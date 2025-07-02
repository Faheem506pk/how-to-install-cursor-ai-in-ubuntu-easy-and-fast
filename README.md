# 🚀 Seamless Cursor AI Installation Guide – Ubuntu AppImage Setup

<p align="center">
  <img src="./cursor.png" alt="Cursor AI Logo" width="200"/>
</p>



> 🎯 *Guide written by [Faheem](https://github.com/faheem506pk) – a passionate Full Stack Web Developer from Pakistan. *



## 🖥️ Install Cursor AI (.AppImage) on Ubuntu – Quick & Easy


### ✅ Prerequisites
- Ubuntu OS installed
- `.AppImage` file for Cursor AI downloaded

---

### 📥 Step 1: Download Cursor AI AppImage


Rename the downloaded file:

```bash
cursor.appimage
````

---

### 📁 Step 2: Make it executable

```bash
cd ~/Downloads
chmod a+x cursor.appimage
```

---

### 📦 Step 3: Install required FUSE package

```bash
sudo apt install libfuse2
```

---

### 🚚 Step 4: Move AppImage to system directory

```bash
sudo mv cursor.appimage /opt/cursor.appimage
```

---

### 🖼️ Step 5: Create a Desktop Entry

```bash
sudo nano /usr/share/applications/cursor.desktop
```

Paste this (replace `faheem506pk` with your actual username if needed):

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

### 🖱️ Step 6: Create a global CLI command

```bash
sudo nano /usr/local/bin/cursor
```

Paste:

```bash
#!/bin/bash
/opt/cursor.appimage "$@" > /dev/null 2>&1 &
```

Then:

```bash
sudo chmod +x /usr/local/bin/cursor
```

---

### 🔐 Step 7: Set up AppArmor profile

```bash
sudo nano /etc/apparmor.d/cursor-appimage
```

Paste this:

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

Then apply:

```bash
sudo apparmor_parser -r /etc/apparmor.d/cursor-appimage
```

---

### ✅ Step 8: Launch Cursor AI from anywhere

```bash
cursor
```

---

## ❓ Cursor Icon Not Showing?

Make sure the icon image exists:

```
/home/faheem506pk/.local/share/icons/cursor.png
```

If not showing:

* ✅ Check it’s a valid `.png` file
* ✅ Run: `chmod 644 cursor.png`
* ✅ Optional: `update-desktop-database`

---

## 🙌 Author

**Muhammad Faheem Iqbal**
👨‍💻 Full Stack Web Developer
🌐 [GitHub](https://github.com/faheem506pk)

---

Enjoy faster coding with **Cursor AI on Ubuntu**! 🚀
*Feel free to star ⭐ this repo if it helped you.*
