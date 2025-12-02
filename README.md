# 🐝 **ServerHive — Shared Bare-Metal Build Servers**

Welcome to **ServerHive**! This guide will walk you through everything you need to know to start using your **enterprise-grade shared bare-metal build server**. 🚀🐝

---

## ⚡ What We Offer

ServerHive provides **raw-performance** shared dedicated servers designed for serious Android/ROM development.

### 🤔 Why Not VPS Instances?

Because virtual machines can’t match **bare-metal power**.
We want you to experience *true performance* with no hypervisor bottlenecks.

> 💬 **Need a fully dedicated instance?**
> We can arrange one on request.

🔒 **We are being strictly monitored by our cloud provider for illegal or abusive usage** — we invest heavily to keep the ecosystem clean and fast.

---

## 🧰 ServerHive Features

Enjoy a powerful ecosystem built for developers:

* ⏸️ **Pause / Resume Plans** – Take breaks without losing days
* 📁 **ServerHive Drive** – Lifetime free storage with fast speeds
* 🖥️ **CodeServer Access** – Full web IDE in your browser
* 📡 **Live Build Tracking** – Watch builds in real-time
* 📱 **ServerHive Mini-App** – Manage from your phone
* 💳 **Wallet Integration** – Easy payments & balance
* 🔔 **Group Alerts & Push Notifications** – Always stay updated
* 📦 **Multiple ROM Sources** – Keep multiple repos without hassle
* 📤 **Auto-Upload** – Completed builds auto-upload to Drive/GoFile

> ℹ️ **Some features vary by plan type. Always confirm with admins.**

---

## 🧩 Getting Started

You’ll receive your SSH credentials once your server is ready.

### Recommended SSH Clients

📱 **Android:** Termux
💻 **Cross-platform:** Termius
🖥️ **PC:** Any standard SSH client

### Example Login

```bash
ssh username@server.serverhive.com -p22
```

---

# 🔨 Complete Build Workflow

Each ROM must run in **its own Byobu session** to prevent conflicts.

---

## 🔧 Step 1: Configure Git Settings

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

## 🍪 Step 2: Set Up Git Cookies (Highly Recommended)

Google rate-limits high concurrency syncs, leading to **429 errors**.
Git cookies fix this. ⚡

### ✨ Benefits:

* Avoids corrupt checkouts
* Reduces quota usage
* Improves sync reliability

### 🔍 How to Generate Git Cookies

1. Open: [https://android.googlesource.com/](https://android.googlesource.com/)
2. Click **Generate Password**
3. Go to **Configure Git**
4. Copy the Linux (bash) script
5. Run it in your terminal

Example:

```bash
touch ~/.gitcookies
chmod 0600 ~/.gitcookies
git config --global http.cookiefile ~/.gitcookies
```

### ❌ Don’t want cookies?

```bash
git config --global http.cookiefile ""
```

---

## 📁 Step 3: Initialize ROM Repository

```bash
mkdir -p ~/lineageos
cd ~/lineageos

repo init -u https://github.com/LineageOS/android.git -b lineage-21.0 --git-lfs
```

(Optional: depth)

```bash
repo init -u https://github.com/LineageOS/android.git -b lineage-21.0 --git-lfs --depth=1
```

---

## 🔄 Step 4: Sync the Source

```bash
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
```

For optimized syncs:

```bash
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune
```

---

## 📦 Step 5: Source the Build Environment

⚠️ **Always do this in a new session.**

```bash
cd ~/lineageos
source build/envsetup.sh
```

---

## 🏗️ Step 6: Build Your ROM

```bash
breakfast <device_codename>
brunch <device_codename>
```

Or:

```bash
mka bacon
```

🚫 **Avoid using `make`.**

---

## 🖥️ Byobu (Sticky Screen)

When you log in, you're already inside a **persistent Byobu session**.

### 🎁 What This Means:

Even if you:

* lose network
* close your terminal
* disconnect accidentally

➡️ **Your build keeps running.**

### ✨ Basic Commands

```bash
# Detach
F6 or Ctrl+a d

# List sessions
byobu-select-session

# Reattach
byobu

# New window
F2

# Switch windows
F3 / F4
```

📱 **In Termux:**
Use **Volume Up + Number**

* Vol+2 → F2
* Vol+3 → F3
* Vol+4 → F4
* Vol+6 → F6

---

## 🗃️ Managing Multiple ROMs

⚠️ **NEVER reuse a Byobu session for a different ROM.**

Each ROM uses different:

* build scripts
* env variables
* paths

### Example:

```bash
# Session 1 - LineageOS
byobu-screen -S lineageos-build
cd ~/lineageos
source build/envsetup.sh
brunch device
```

```bash
# Session 2 - PixelExperience
byobu-screen -S pixelexperience-build
cd ~/pixelexperience
source build/envsetup.sh
brunch device
```

---

## 🔐 Root Access

Root is **not provided** because most packages are already preinstalled.

Need something installed?
Just ask the admin. 😄

Example:

```
Hi, can you please install the following?
Command: sudo apt install <package-name>
```

---

## ⏳ Plan Expiration

🗑️ After your plan expires, **all data is auto-deleted**.

### ❤️ Need More Time?

Click **“Extend my plan by 2 hours”** once per rental — totally FREE.

⚠️ You can use this **only once**.

---

## 💡 Quick Tips

✔️ Create separate Byobu sessions per ROM
✔️ Always run builds inside Byobu
✔️ Set up Git cookies
✔️ Track builds via dashboard
✔️ Use ServerHive Drive for uploads
✔️ Ask admin for missing packages
✔️ Remember expiration cleanup
✔️ Use the free 2-hour extension wisely

---

## 🧭 Typical Workflow Summary

```bash
# 1. Create a session
tmux or byobu # (ignore if you're already present in a tmux or byobu session)

# 2. Configure git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 3. Setup git cookies

# 4. Init repo
mkdir ~/rom-name && cd ~/rom-name
repo init -u <manifest-url> -b <branch>

# 5. Sync
repo sync -c -j$(nproc --all) --force-sync

# 6. Source env
source build/envsetup.sh

# 7. Build
breakfast <device>
brunch <device>
```

---

## 🆘 Support

Need help? We’re always here! 💬

* [ServerHive Group](t.me/ServerRentals)
* [ServerHive Owner](t.me/Shra1V32)

---

## 🎉 Happy Building!

You're now ready to enjoy the full ServerHive experience.
Build fast. Build clean. Build smart. 🐝🔥🚀
