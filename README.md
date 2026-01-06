# 🐝 **ServerHive — Enterprise Bare-Metal Build Environment**

Welcome to **ServerHive**! This guide provides the essential knowledge to maximize your productivity on our **enterprise-grade shared bare-metal build servers**. Designed specifically for high-performance Android and ROM development, ServerHive eliminates the bottlenecks of traditional virtualization. 🚀🐝

---

## ⚡ The ServerHive Advantage

We provide **raw, native performance** on dedicated hardware. Unlike VPS instances, our bare-metal architecture ensures that every cycle of the CPU is dedicated to your build tasks, with no hypervisor overhead.

### Why Bare-Metal?
Virtual machines often suffer from "noisy neighbor" effects and I/O latency. Our environment is optimized for the intense multi-threaded workloads required for modern ROM compilation.

> 💬 **Need a fully dedicated instance?** 
> Private, non-shared servers are available upon request for enterprise users.

🔒 **Security & Policy:** Our infrastructure is strictly monitored for compliance. We maintain a zero-tolerance policy for illegal or abusive usage to ensure a clean, high-speed ecosystem for all legitimate developers.

---

## 🧰 Key Features

* ⏸️ **Flexible Billing** – Pause and resume your plans to save your balance.
* 📁 **ServerHive Drive** – High-speed, permanent storage for your assets.
* 🖥️ **Integrated IDE** – Access a full CodeServer (VS Code) instance directly in your browser.
* 📡 **Real-Time Monitoring** – Track build progress and system health through our dashboard.
* 📱 **Mobile Management** – Use our Mini-App to manage your server on the go.
* 💳 **Unified Wallet** – Seamless payments and automated balance management.
* 🛡️ **Automated Verification** – AI-powered instant payment verifications for credits.
* 📤 **Automated Deployment** – Auto-upload completed builds to Drive or GoFile.

---

## 🧩 Getting Started

Your SSH credentials will be delivered via your dashboard or admin once your environment is provisioned.

### Recommended SSH Clients
* 📱 **Mobile:** [Termux](https://termux.dev/) (Android) or [Ish](https://ish.app/) (iOS)
* 💻 **Desktop:** [Termius](https://termius.com/), [PuTTY](https://www.putty.org/), or your native system terminal.

### Accessing Your Server
```bash
ssh username@server.serverhive.com -p 22
```

---

# 🔨 The Build Workflow

To maintain stability in a shared environment, all builds **must** be executed within a persistent session.

---

## 🔧 Step 1: Global Git Configuration
Set up your identity before starting any repository operations.
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

## 🍪 Step 2: Git Cookies (Performance Optimization)
Google implements aggressive rate-limiting on unauthenticated high-concurrency syncs, often resulting in **429 Too Many Requests** errors. Using Git cookies is highly recommended to ensure reliable synchronization. ⚡

### Benefits
* Prevents sync-interrupting rate limits.
* Reduces metadata overhead.
* Improves checkout reliability for large manifests.

### Setup Instructions
1. Visit [android.googlesource.com](https://android.googlesource.com/).
2. Click **"Generate Password"**.
3. Authenticate and follow the **"Configure Git"** instructions.
4. Copy and execute the provided shell script in your terminal.

---

## 📁 Step 3: Initialize Repository
```bash
mkdir -p ~/lineageos && cd ~/lineageos

# Standard initialization
repo init -u https://github.com/LineageOS/android.git -b lineage-21.0 --git-lfs

# Shallow clone (Faster, saves space)
repo init -u https://github.com/LineageOS/android.git -b lineage-21.0 --git-lfs --depth=1
```

---

## 🔄 Step 4: Synchronize Source
Use the following command for an optimized, high-speed sync:
```bash
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune
```

---

## 📦 Step 5: Environment Setup
⚠️ **Note:** Always source your environment in a clean shell session to avoid variable pollution.
```bash
source build/envsetup.sh
```

---

## 🏗️ Step 6: Execute Build
```bash
# Select your device
breakfast <device_codename>

# Start compilation
brunch <device_codename>
# OR
mka bacon
```
🚫 **Pro Tip:** Avoid using generic `make`. Use `mka` or `brunch` for optimized resource allocation.

---

## 🖥️ Persistent Sessions (Byobu/Tmux)

ServerHive uses **Byobu** as the default terminal multiplexer. When you login, you are automatically placed in a persistent session.

### The Power of Persistence
If your connection drops or you close your terminal, **your build continues to run**. You can reattach at any time from any device.

### Essential Commands
* **Detach:** `F6` or `Ctrl+a` then `d`
* **New Window:** `F2`
* **Navigate Windows:** `F3` (Previous) / `F4` (Next)
* **Reattach:** Simply type `byobu` after logging back in.

---

## 🗃️ Multi-ROM Management
⚠️ **Constraint:** Never attempt to build two different ROMs within the same window or environment session. This will cause dependency conflicts.

**Recommended Workflow:**
1. Create a new Byobu window (`F2`).
2. Navigate to your second ROM directory.
3. Source the environment and start your build.

---

## 🔐 Root Access & Package Management

Standard **root access is not provided** for security and stability reasons. However, our environment is pre-configured with 99% of the tools you will ever need for Android development.

### Developing Without Root (The 90/10 Rule)
90% of development tasks on Linux **do not require root**. You can install local binaries, manage Python environments with `venv` or `uv`, and use Node.js via `nvm`—all within your home directory.

**If you think you need root, try this first:**
* Ask an AI (like Claude or ChatGPT): *"How can I install [Tool Name] on Linux without sudo access?"*
* Most tools can be compiled from source or downloaded as pre-compiled binaries into `~/bin`.

### Requesting System Packages
If a specific system-level dependency is missing, simply contact an admin:
> "Hi, could you please install `libncurses5` via `sudo apt install`? It's required for my legacy build."

---

## ⏳ Plan Expiration & Extensions
To keep our high-performance storage clean, **data is automatically purged** upon plan expiration.

### The "Safety Net" Extension
Need a bit more time to finish a sync or upload? You can extend any rental by **2 hours for FREE**.
* This can be claimed once per rental via the dashboard.
* Use it wisely when your build is at 95%!

---

## 🆘 Support & Community
Join our community for tips, tricks, and technical support.
* 📢 **Telegram Group:** [t.me/ServerRentals](https://t.me/ServerRentals)

---

## 🎉 Happy Building!
You are now equipped with the power of ServerHive. Build faster, cleaner, and smarter. 🐝🔥🚀
