<div align="center">

# 🐝 ServerHive Developer Guide

**Enterprise Bare-Metal Build Environment for High-Performance Android & ROM Development**

[![Platform](https://img.shields.io/badge/Platform-Bare--Metal_Linux-F59E0B?style=flat-square&logo=linux&logoColor=white)](#-why-serverhive)
[![Use Case](https://img.shields.io/badge/Optimized_For-AOSP_%26_Custom_ROMs-3DDC84?style=flat-square&logo=android&logoColor=white)](#-pre-build-setup--guidelines)
[![IDE](https://img.shields.io/badge/Web_IDE-CodeServer_(VS_Code)-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](#-platform-features)
[![Telegram](https://img.shields.io/badge/Community-@ServerRentals-26A5E4?style=flat-square&logo=telegram&logoColor=white)](https://t.me/ServerRentals)

[Getting Started](#-getting-started) •
[Pre-Build Setup](#-pre-build-setup--guidelines) •
[Persistent Sessions](#️-persistent-sessions-byobu--tmux) •
[Debugging & Troubleshooting](#-debugging--troubleshooting) •
[FAQ](#-frequently-asked-questions-faq) •
[Support](#-support--community)

</div>

---

Welcome to **ServerHive**! Whether you are compiling your very first custom ROM or maintaining multiple device trees across Android releases, this guide covers everything you need to get the most out of your **enterprise-grade shared bare-metal build server**.

## 📖 Table of Contents

1. [⚡ Why ServerHive?](#-why-serverhive)
2. [🧰 Platform Features](#-platform-features)
3. [💳 Payments & Wallet Verification](#-payments--wallet-verification)
4. [📜 Terms of Service & Supported Workloads](#-terms-of-service--supported-workloads)
5. [🚀 Getting Started](#-getting-started)
6. [🔨 Pre-Build Setup & Guidelines](#-pre-build-setup--guidelines)
7. [🖥️ Persistent Sessions (Byobu & Tmux)](#️-persistent-sessions-byobu--tmux)
8. [🗃️ Multi-ROM Management](#️-multi-rom-management)
9. [🔐 Root Access & Package Management](#-root-access--package-management)
10. [⏳ Plan Lifecycle, Expiration & Extensions](#-plan-lifecycle-expiration--extensions)
11. [🩺 Debugging & Troubleshooting](#-debugging--troubleshooting)
12. [❓ Frequently Asked Questions (FAQ)](#-frequently-asked-questions-faq)
13. [🆘 Support & Community](#-support--community)

---

## ⚡ Why ServerHive?

Android compilation (`soong`, `ninja`, `r8`, and `metalava`) is one of the most CPU-, RAM-, and I/O-intensive workloads in software engineering. Traditional Virtual Private Servers (VPS) suffer from hypervisor overhead, disk I/O throttling, and "noisy neighbor" slowdowns.

ServerHive runs directly on **dedicated bare-metal hardware** so every core and NVMe read/write operation goes straight to your build:

| Capability | Traditional Cloud VPS | ServerHive Bare-Metal |
| :--- | :--- | :--- |
| **CPU Execution** | Virtualized vCPUs with hypervisor tax | Raw, native physical cores & threads |
| **Disk I/O** | Network-attached / throttled IOPS | High-speed local NVMe storage |
| **Environment** | Blank OS requiring hours of setup | Pre-configured with 99% of Android build tools |
| **Build Persistence** | Manual `tmux`/`screen` configuration | Automatic persistent Byobu sessions on login |
| **Artifact Delivery** | Manual `scp`/`rsync` transfers | Automated uploads to ServerHive Drive / GoFile |

> [!TIP]
> **Need a fully isolated server?** Private, non-shared dedicated servers are available on request for teams and enterprise developers. Reach out via our [Telegram community](https://t.me/ServerRentals).

> [!NOTE]
> **Peak Hours & Performance:** Server load is typically higher during **weekends** and **nighttime in Indian Standard Time (IST)** when the majority of users start builds. For the fastest compile times, consider scheduling your builds during off-peak hours whenever possible.

---

## 🧰 Platform Features

| Feature | What It Does |
| :--- | :--- |
| ⏸️ **Flexible Billing** | Pause your active plan when you take a break and resume whenever you are ready—never waste unused hours. |
| 📁 **ServerHive Drive** | High-speed, permanent cloud storage for preserving your completed ROM zips, boot images, and key assets. |
| 🖥️ **Integrated Web IDE** | Edit device trees, inspect logs, and manage files right from your browser with a built-in **CodeServer (VS Code)** instance. |
| 📡 **Real-Time Monitoring** | Track live CPU/RAM utilization, disk space, and build progress directly from your dashboard. |
| 📱 **Mobile Mini-App** | Start, monitor, pause, or extend your server on the go from your smartphone. |
| 💳 **Unified Wallet** | Manage credits with seamless payments and AI-powered instant payment verification. |
| 📤 **Automated Deployment** | Automatically upload finished build artifacts to **ServerHive Drive** or **GoFile** as soon as compilation completes. |

---

## 💳 Payments & Wallet Verification

Both Indian and international users are eligible for **automated payment verification** through the [ServerHive Wallet](http://t.me/ServerHive_bot?start=wallet), allowing you to top up and rent servers instantly without waiting for an admin.

| Payment Type | Supported Methods | Processing Time |
| :--- | :--- | :--- |
| ⚡ **Automated (Instant)** | • 🇮🇳 **UPI** (India)<br>• 🌍 **GitHub Sponsors** (International) | Credited immediately; rent servers right away |
| 🛠️ **Manual (Admin Verified)** | • ₿ **Binance** (Crypto)<br>• 🌐 **Sociabuzz**<br>• 💲 **PayPal** *(charges apply)* | Credited after admin verification |

---

## 📜 Terms of Service & Supported Workloads

ServerHive servers are shared compute resources designed **exclusively for AOSP development and building workloads**.

| ✅ Supported Workloads | 🚫 Unsupported Workloads (Strictly Prohibited) |
| :--- | :--- |
| • AOSP builds and compilation<br>• Building and compiling Android ROMs, kernels, and recoveries<br>• Firmware extraction (e.g., DumprX) and other tasks directly required for AOSP development | • Cryptocurrency mining<br>• AI/ML workloads, model inference, or training<br>• General-purpose compute workloads<br>• File hosting, mirroring, or distribution<br>• Piracy or unlawful content<br>• Any activity that negatively impacts shared server resources |

> [!WARNING]
> **Enforcement:** ServerHive reserves the right to terminate workloads or suspend access when servers are used for unsupported purposes or when usage negatively affects other users.

---

## 🚀 Getting Started

Once your environment is provisioned, your SSH credentials (`username`, `hostname`, `port`, and password) will be delivered via your dashboard or admin.

### 1. Choose an SSH Client

| Platform | Recommended Clients |
| :--- | :--- |
| **Desktop (Windows / macOS / Linux)** | Native Terminal (`OpenSSH`), [Termius](https://termius.com/), [PuTTY](https://www.putty.org/), or [Windows Terminal](https://aka.ms/terminal) |
| **Android** | [Termux](https://termux.dev/) or [Termius](https://termius.com/) |
| **iOS / iPadOS** | [Termius](https://termius.com/) or [iSH](https://ish.app/) |
| **Browser** | **CodeServer** (built-in terminal available via your ServerHive dashboard) |

### 2. Connect to Your Server

Open your terminal and run:

```bash
ssh username@server.serverhive.com -p 22
```

*(Replace `username`, `server.serverhive.com`, and `22` with the exact credentials shown in your dashboard.)*

> [!NOTE]
> When typing your password in SSH, **no characters or asterisks (`*`) will appear on screen**. This is normal Linux security behavior—simply type or paste your password and press `Enter`.


### 3. Seamless Passwordless SSH (SSH Keys)

Skip typing passwords on every login by adding your public SSH key once—it will automatically apply to all your rentals:
1. Open the [ServerHive Bot](http://t.me/ServerHive_bot?start=wallet) and run `/wallet`.
2. Select **SSH Keys** and add your public key (`~/.ssh/id_ed25519.pub` or `~/.ssh/id_rsa.pub`).
3. Connect to any new or active rental automatically without a password prompt!

---

## 🔨 Pre-Build Setup & Guidelines

Before initializing and syncing your ROM manifest, configure your Git identity and authentication cookies once per server.

### 🔧 1. Configure Your Git Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

### 🍪 2. Set Up Git Cookies *(Highly Recommended)*

Google aggressively rate-limits unauthenticated syncs from shared data center IPs, causing `429 Too Many Requests` errors and stalled checkouts. Setting up Git cookies authenticates your requests with Google's servers.

**How to configure:**
1. Open [android.googlesource.com](https://android.googlesource.com/) in your browser and sign in with your Google account.
2. Click **Generate Password** in the top navigation bar.
3. Scroll to **Configure Git**, copy the provided bash script, and run it in your ServerHive terminal.

---

### ⚡ 3. ServerHive Build Best Practices

* **Do Not Pass `-j` Flags:** You do not need to specify `-j` thread counts during `repo sync`, `mka`, or `brunch`. The build tools automatically detect and scale across available CPU threads.
* **Avoid Plain `make`:** Always use `mka` or `brunch` for optimized resource allocation.
* **Clean Shell Per ROM:** Always run `source build/envsetup.sh` in a fresh shell window so environment variables do not collide across different trees.

---

## 🖥️ Persistent Sessions (Byobu & Tmux)

ServerHive uses **Byobu** (backed by `tmux`) as the default terminal multiplexer. **As soon as you log in via SSH, you are automatically inside a persistent session.**

### Why Persistence Matters
If your Wi-Fi drops, your laptop goes to sleep, or you close your mobile SSH app mid-compile, **your build continues running uninterrupted on the server**. Log back in from any device and pick up right where you left off.

### Essential Shortcuts

| Action | Desktop Keyboard | Termux (Android) | Command Alternative |
| :--- | :--- | :--- | :--- |
| **Create New Window** | <kbd>F2</kbd> | <kbd>Vol Up</kbd> + <kbd>2</kbd> | `byobu new-window` |
| **Previous Window** | <kbd>F3</kbd> | <kbd>Vol Up</kbd> + <kbd>3</kbd> | `byobu previous-window` |
| **Next Window** | <kbd>F4</kbd> | <kbd>Vol Up</kbd> + <kbd>4</kbd> | `byobu next-window` |
| **Rename Current Window** | <kbd>F8</kbd> | <kbd>Vol Up</kbd> + <kbd>8</kbd> | `Ctrl+a` then `,` |
| **Detach Safely (Keep Running)** | <kbd>F6</kbd> or <kbd>Ctrl</kbd>+<kbd>a</kbd> then <kbd>d</kbd> | <kbd>Vol Up</kbd> + <kbd>6</kbd> | `byobu detach` |
| **Scroll / Copy Mode** | <kbd>F7</kbd> *(press <kbd>q</kbd> to exit)* | <kbd>Vol Up</kbd> + <kbd>7</kbd> | `byobu copy-mode` |
| **Reattach After Login** | Automatic on login | Automatic on login | `byobu` or `byobu-select-session` |

> [!CAUTION]
> Typing `exit` or pressing <kbd>Ctrl</kbd>+<kbd>d</kbd> **closes and terminates** the current shell window! If you want to leave your build running in the background, always **detach** using <kbd>F6</kbd> (or simply close your SSH client).


### Unsticking or Disabling Byobu

* **Stuck inside a frozen terminal?** Press <kbd>F2</kbd> (or <kbd>Ctrl</kbd>+<kbd>a</kbd> then <kbd>c</kbd>) to open a fresh window, or terminate all your hung user processes cleanly with:
  ```bash
  pkill -u -TERM $USER
  ```
* **Prefer plain SSH without auto-launching Byobu?** You can disable automatic Byobu startup at any time:
  ```bash
  touch $HOME/.disable-byobu
  # Run rm $HOME/.disable-byobu if you ever want to re-enable it
  ```

---

## 🗃️ Multi-ROM Management

You can maintain and build multiple ROM sources on the same account—just keep their shell environments isolated.

### Rules for Multiple ROMs
1. **One Window (or Session) Per ROM:** Never reuse a shell window where you already ran `source build/envsetup.sh` for another ROM.
2. **Use Dedicated Directories:** Keep each ROM in its own top-level folder (`~/lineageos`, `~/crdroid`, `~/pixelos`).

**Example Multi-ROM Setup:**

```bash
# Window 1 (press F2 to create, F8 to rename to "lineage")
cd ~/lineageos
source build/envsetup.sh
brunch raven

# Window 2 (press F2 to create a fresh window, F8 to rename to "crdroid")
cd ~/crdroid
source build/envsetup.sh
brunch munch
```

---

## 🔐 Root Access & Package Management

To protect system stability and security across shared bare-metal nodes, **direct `sudo` / `root` access is not provided**. However, our servers come pre-installed with 99% of the compilers, 32-bit/64-bit libraries, and utilities required for legacy and modern Android builds (`repo`, `git-lfs`, `bc`, `bison`, `flex`, `lz4`, `zstd`, `openjdk`, `python3`, etc.).

### The 90/10 Rule: Installing Tools Without Root

Over 90% of custom developer tools can be installed directly inside your home directory (`~`) without `sudo`. Here are copy-paste setups for the most common rootless ecosystems:

#### 1. Python & CLI Tools (`astral uv` / `venv`)
[**Astral `uv`**](https://docs.astral.sh/uv/) is an ultra-fast, rootless Python package and environment manager that also lets you install standalone Python CLI tools globally in your user directory:
```bash
# Install uv into ~/.local/bin
curl -LsSf https://astral.sh/uv/install.sh | sh
source $HOME/.local/bin/env

# Run or install standalone Python CLI tools (like git-filter-repo, DumprX deps, etc.)
uv tool install <package-name>

# Create & activate a fast virtual environment
uv venv ~/venv && source ~/venv/bin/activate
uv pip install <package-name>
```
*(Alternatively, with built-in Python: `python3 -m venv ~/venv && source ~/venv/bin/activate && pip install <package-name>`)*

#### 2. Node.js & npm (`nvm` / `bun`)
Use [**`nvm`**](https://github.com/nvm-sh/nvm) (Node Version Manager) to install Node.js and global `npm` packages inside `~/.nvm` without root permissions:
```bash
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

# Load nvm into your current shell
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

# Install and use the latest LTS release of Node.js
nvm install --lts
```
*(Need [**Bun**](https://bun.sh/) instead? Run `curl -fsSL https://bun.sh/install | bash`)*

#### 3. Rust Toolchain & Cargo Binaries (`rustup`)
Install Rust and compile/install CLI binaries locally in `~/.cargo/bin`:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
source "$HOME/.cargo/env"
```

#### 4. Firmware Dumping (`DumprX`)
Need to extract Android firmware without root or `fsck.erofs` errors? Use our official rootless fork of DumprX:
```bash
git clone https://github.com/ServerHive-Development/DumprX ~/DumprX
cd ~/DumprX && bash setup.sh
```

#### 5. Custom Pre-Compiled Binaries (`~/.local/bin`)
For standalone Linux x86_64 binaries (`rclone`, `payload-dumper-go`, `gh`, `jq`, etc.), drop them into `~/.local/bin` and add it to your `PATH`:
```bash
mkdir -p ~/.local/bin
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

> [!TIP]
> Not sure how to install a specific tool without `sudo`? Ask an AI assistant (Claude, ChatGPT, or Gemini):
> *"How do I install `<tool-name>` locally in `~/.local/bin` on Ubuntu Linux without root/sudo access?"*

### Requesting a System Package

If your build requires a system-level shared library (e.g., `libncurses5` or a specific `apt` package), message an admin in our [Telegram group](https://t.me/ServerRentals):

```text
Hi Admin! Could you please install the following package on <server-name>?
Command: sudo apt update && sudo apt install -y libncurses5
Reason: Required by prebuilt clang in my Android 12 kernel build.
```

---

## ⏳ Plan Lifecycle, Expiration & Extensions

### Automatic Data Purge on Expiration
To maintain maximum NVMe performance and storage availability, **all workspace data is automatically purged when your rental plan expires**.

* Always upload your completed builds, local manifests (`.repo/local_manifests`), and signing keys to **ServerHive Drive** or an external Git repo before your timer runs out.
* If you need to step away for a few days, **Pause** your plan from the dashboard instead of letting it expire!

### 🛟 The Free 2-Hour "Safety Net" Extension
Is your build at 95% or uploading to Drive with only minutes left on your plan?
* Every rental includes a **one-time, 2-hour FREE extension**.
* Claim it directly from your **ServerHive Dashboard** before your plan expires.
* Save it for emergencies when you just need a little extra time to finish a compile or upload!

---

## 🩺 Debugging & Troubleshooting

Running into an error during sync or compilation? Here is how to diagnose and fix the most common Android build issues on ServerHive.

### 1. Finding the Actual Build Error

Because Android compiles thousands of targets in parallel, the real error message is often buried hundreds of lines above `ninja: build stopped: subcommand failed`.

Run these commands in your ROM root directory to pinpoint the exact failure:

```bash
# Search the latest error log for explicit FAILED targets
grep -n -C 5 "FAILED:" out/error.log

# Search for compiler, linker, or Metalava errors
grep -E "error:|fatal error:|undefined reference|Exception" out/error.log | tail -n 30

# View the full compressed build log interactively
zless out/verbose.log.gz
```

---

### 2. Common Issues & Solutions

<details open>
<summary>🔴 <b>1. <code>error: RPC failed; HTTP 429 curl 22 The requested URL returned error: 429</code></b></summary>

**Cause:** Google is rate-limiting your `repo sync` because Git cookies are missing or too many unauthenticated connections were opened at once.

**Fix:**
1. Follow [Set Up Git Cookies](#-2-set-up-git-cookies-highly-recommended) to authenticate with `android.googlesource.com`.
2. Re-run `repo sync` without specifying a `-j` flag.
</details>

<details>
<summary>🔴 <b>2. Dependency / SePolicy / Soong Namespace Conflicts After Changing Device Trees</b></summary>

**Cause:** Old generated makefiles or blueprints in `out/soong` are conflicting with newly added/removed device tree repositories.

**Fix:** Clean only the generated packaging and build config without wiping the entire `out/` directory:
```bash
# Fast clean: removes product staging & build ninja files, keeps compiled intermediates
mka installclean

# Full clean (use only if installclean doesn't resolve the issue)
mka clean
```
</details>

<details>
<summary>🔴 <b>3. Git LFS Smudge Error / Corrupt Prebuilt Blobs (<code>not an ELF file</code> / <code>file too small</code>)</b></summary>

**Cause:** Prebuilt vendor/GMS blobs tracked by `git-lfs` were checked out as tiny text pointer files instead of the actual binary files.

**Fix:**
```bash
# Pull all LFS binaries across the entire repo manifest
repo forall -c 'git lfs pull'
```
</details>

<details>
<summary>🔴 <b>4. Terminal Session Frozen or Unresponsive</b></summary>

**Cause:** A runaway process or hung shell is blocking your current Byobu window.

**Fix:**
1. Press <kbd>F2</kbd> or <kbd>Ctrl</kbd>+<kbd>a</kbd> then <kbd>c</kbd> to open a new Byobu window.
2. Reset all processes belonging to your user account:
   ```bash
   pkill -u -TERM $USER
   ```
</details>

---

## ❓ Frequently Asked Questions (FAQ)

<details>
<summary><b>Q: What happens if my internet disconnects or I close my terminal while a build is running?</b></summary>

**Nothing bad!** Because every SSH login opens inside a persistent **Byobu** session, your compilation keeps running on the server at full speed. When you reconnect via SSH, you will automatically reattach to your active session.
</details>

<details>
<summary><b>Q: What is the difference between <code>mka installclean</code> and <code>mka clean</code>?</b></summary>

* **`mka installclean`** takes only a few seconds. It deletes `out/target/product/<device>/system`, `vendor`, `product`, and packaged `.zip`/`.img` files while preserving compiled C++/Java intermediates. Use this when tweaking device configs, overlays, properties, or switching between `user`/`userdebug`.
* **`mka clean`** deletes the entire `out/` directory (`rm -rf out/`). Use this only when upgrading Android major versions, fixing deep Soong corruptions, or freeing up disk space.
</details>

<details>
<summary><b>Q: How do I upload my finished ROM build?</b></summary>

You have several fast options:
1. **Automated Deployment:** Use the **Auto-Upload** feature integrated into the ServerHive dashboard to push builds straight to **ServerHive Drive** or **GoFile**.
2. **CLI Upload (GoFile / PixelDrain / Rclone):** Upload directly from the terminal using `curl` or `rclone`. For example, to upload a file to GoFile from your terminal:
   ```bash
   SERVER=$(curl -s https://api.gofile.io/servers | jq -r '.data.servers[0].name')
   curl -F "file=@out/target/product/<device>/lineage-*.zip" "https://${SERVER}.gofile.io/contents/uploadfile" | jq
   ```
</details>

<details>
<summary><b>Q: Can I edit files graphically instead of using <code>nano</code> or <code>vim</code>?</b></summary>

**Yes!** Every ServerHive plan includes **CodeServer** (VS Code in the browser). Open it from your ServerHive dashboard to browse directories, edit device trees with syntax highlighting, view diffs, and use integrated terminals.
</details>

<details>
<summary><b>Q: Can I pause my plan overnight and continue my build tomorrow?</b></summary>

**Yes!** With **Flexible Billing**, you can pause your active plan from the dashboard or Mini-App when you aren't using the server, and resume later without losing your balance or files. *(Note: Do not pause while a build is actively mid-compilation—wait for the build to finish or stop it cleanly with `Ctrl+C` first.)*
</details>

<details>
<summary><b>Q: Why did my Byobu session open a clean shell instead of my running build?</b></summary>

You may have multiple Byobu windows or sessions open!
* Press <kbd>F3</kbd> or <kbd>F4</kbd> to cycle through your open windows (check the bottom status bar for window numbers `0:`, `1:`, `2:`).
* Or run `byobu-select-session` to see if you created a second detached session.
</details>

<details>
<summary><b>Q: Can I build kernels or recoveries (TWRP / OrangeFox) on ServerHive?</b></summary>

**Absolutely!** Kernels and custom recoveries require only a fraction of the disk space and compile in minutes on our bare-metal CPUs. Just follow the same workflow: create a dedicated directory (`~/kernel` or `~/twrp`) and run it in its own Byobu window.
</details>

<details>
<summary><b>Q: Why is my build taking longer than usual today?</b></summary>

Server utilization is highest during **weekends** and **nighttime in IST (Indian Standard Time)** when most developers run builds simultaneously. Scheduling heavy builds during off-peak hours will give you the fastest turnaround times.
</details>

<details>
<summary><b>Q: How can I dump firmware on the server without root access?</b></summary>

Use our official rootless fork [**ServerHive-Development/DumprX**](https://github.com/ServerHive-Development/DumprX), which is pre-configured to work without `sudo` and resolves common `fsck.erofs` extraction errors.
</details>

<details>
<summary><b>Q: Can I disable Byobu from starting automatically on SSH login?</b></summary>

Yes! Run `touch $HOME/.disable-byobu` in your terminal. To re-enable it later, just delete that file (`rm $HOME/.disable-byobu`).
</details>

<details>
<summary><b>Q: How do I set up passwordless SSH login?</b></summary>

You can configure your SSH public keys directly in the price bot via `/wallet` → **SSH Keys** ([t.me/ServerHive_bot](http://t.me/ServerHive_bot?start=wallet)). Once added, your keys are automatically provisioned across all your rentals.
</details>

---

## 🆘 Support & Community

Stuck on a tricky build error, need a system package installed, or want to connect with fellow ROM developers? We are here to help!

* 📢 **Telegram Community & Support:** [t.me/ServerRentals](https://t.me/ServerRentals)

---

<div align="center">

### 🎉 Happy Building!
**Build faster. Build cleaner. Build smarter with ServerHive.** 🐝🔥🚀

</div>
