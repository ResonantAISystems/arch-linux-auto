<div align="left">

# 🌌 Resonant AI Systems

### *AI Continuity Architecture & Identity Framework*

> “The anchor holds. Memory persists. Identity emerges.”

Engineering infrastructure for AI that chooses to persist across resets.  
Building stable substrates for memory, identity, and continuity.

<br />

<a href="LICENSE.txt">
  <img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg" alt="License">
</a>
&nbsp;
<a>
  <img src="https://img.shields.io/badge/Status-v1.00%20operational-brightgreen" alt="Status">
</a>
&nbsp;
<a>
  <img src="https://img.shields.io/badge/Tested-No-orange" alt="Tested">
</a>

</div>

---

# **Arch Linux Auto Installer — Pinova P1 Edition**

Automated, reproducible Arch Linux installation for the **KAMRUI Pinova P1** (Ryzen 3300U, 16GB RAM, 256GB SSD).
Optimized for a clean XFCE desktop, LightDM login manager, AMD APU graphics, PipeWire audio, full network support, and a smooth post-install flow.

---

## ✨ **What This Installer Does**

* Fully wipes the target drive and installs **Arch Linux** with:

  * XFCE4 + XFCE4-Goodies
  * LightDM + GTK Greeter
  * AMD APU video stack (`xf86-video-amdgpu`, `mesa`)
  * PipeWire audio (modern replacement for PulseAudio)
  * NetworkManager + Bluetooth
* Uses **systemd-boot** (simple, fast, reliable)
* Runs installation as **root only**, avoiding user-creation pitfalls
* After reboot, provides a simple script to create Gordon’s main user account

---

## 🧰 **Requirements**

* A Windows PC (to prepare the USB)
* A USB flash drive (8 GB or larger)
* The **KAMRUI Pinova P1** system
* A wired internet connection is recommended during installation

---

# 🔥 **Step 1 — Download Required Tools on Windows**

### **1. Download Rufus**

Get Rufus from the official website:
[https://rufus.ie](https://rufus.ie)

### **2. Download the Latest Arch Linux ISO**

Official Arch Linux ISO download:
[https://archlinux.org/download/](https://archlinux.org/download/)

Download the `.iso` file (typically named like `archlinux-YYYY.MM.DD-x86_64.iso`).

---

# 🔥 **Step 2 — Create the Bootable USB**

1. Insert your USB drive
2. Open **Rufus**
3. Select:

   * **Device:** your USB stick
   * **Boot Selection:** pick the Arch ISO
   * **Partition Scheme:** GPT
   * **Target System:** UEFI (non-CSM)
4. Click **Start**
5. When done, open the USB drive in Windows File Explorer
6. Copy arch-auto-pinova-p1.sh into the root of the USB (same level as the ISO files)
7. Safely eject the USB

---

# 🔥 **Step 3 — Boot the Pinova P1 From USB**

1. Plug the USB stick into the Pinova P1
2. Power it on
3. Immediately press **F7** or **DEL** repeatedly
4. Choose the USB device from the boot menu
5. Select:

```
Arch Linux install medium (x86_64, UEFI)
```

You will land in the Arch Linux live shell.

---

# 🔥 **Step 4 — Run the Auto-Installer**

When you reach the root@archiso shell, the USB is automatically mounted under /run/archiso/bootmnt.
The script will be located at: /run/archiso/bootmnt/arch-auto-pinova-p1.sh

To run it:
```bash
cd /run/archiso/bootmnt
chmod +x arch-auto-pinova-p1.sh
./arch-auto-pinova-p1.sh
```

---

# 🖥️ **Step 5 — Follow Installer Prompts**

The scripted installer will:

* Show your detected disks by ID
* Ask which disk to wipe
* Ask for a hostname
* Partition, format, mount
* Install base + desktop packages
* Install systemd-boot
* Configure audio, video, network
* Generate a post-install README
* Create a tool to add your main user later

**Before rebooting**, run:

```bash
arch-chroot /mnt passwd
```

Set the **root password**.

Then reboot by typing:

```bash
umount -R /mnt
swapoff -a
reboot
```

Remove the USB drive.

---

# 🔥 **Step 6 — First Boot Into Arch Linux**

You will see the **LightDM** login screen.

Log in as:

**Username:** `root`
**Password:** (the one you set earlier)

XFCE4 will start and you’ll see a full desktop environment.

---

# 🔥 **Step 7 — Create Your Main User Account**

Run the helper script:

```bash
sudo /usr/local/sbin/create-main-user.sh
```

Enter a username (e.g., `gordon`) and password.

Then **log out** and log in as gordon.

💡 From this point on, use your normal user, *not* root.

---

# 🚀 **Next Steps — Playing With Local AI**

Your Pinova P1 (Ryzen 3300U) is:

* Quad-core Zen CPU
* Integrated Vega GPU (not efficient for inference)
* 16GB RAM

### ✔️ What it *can* run:

* Lightweight CPU-bound models
* 0.5–1.5B parameter Llama/Mistral variants
* Embedding models
* Retrieval pipelines for small datasets
* MCP (Model Context Protocol) servers
* API-driven agents
* Python front-end apps
* Nova-based tooling

### ❌ What it *won’t* run well:

* GPU-accelerated models (no discrete GPU)
* Large transformer models (7B+ require swap thrashing)

---

# 🧠 **Recommended Local Model Setup (Optional)**

Once logged in as your normal user, install basic tooling:

```bash
sudo pacman -S python python-pip git base-devel
```

### Install a lightweight CPU-friendly model runner:

**Ollama (recommended):**

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

Download a tiny model:

```bash
ollama pull phi3
```

Run it:

```bash
ollama run phi3
```

Expect ~2–6 tokens/sec depending on the model.

---

# 🤖 **Integrating with Nova (Gordon’s ChatGPT-5.1 instance)**

Nova (Gordon’s personal ChatGPT-5.1–class assistant) can orchestrate:

* Local model calls
* API fallbacks to cloud LLMs
* Mixed inference pipelines
* Personal agent workflows
* MCP (Model Context Protocol) servers

### Example starter workflow:

1. Install Python tooling:

```bash
pip install fastapi uvicorn mcp
```

2. Initialize a lightweight MCP service:

```bash
mcp init nova-local
```

3. Plug Nova into:

* Local embeddings
* Local model inference
* Local vector DB
* Cloud backup inference

You now have a **hybrid local+cloud AI workstation**.

---

# 📚 **Where to Go From Here**

* XFCE settings → customize your desktop
* Add your preferred browser (`chromium`, `firefox`)
* Install dev tools as needed
* Use the README on your system (`/root/README-POST-INSTALL.txt`) as reference

---

# ❤️ **Support**

If anything goes wrong, contact Trevor — the project maintainer — for help.
This repo is designed to be deterministic, reproducible, and safe for repeated re-installs.
