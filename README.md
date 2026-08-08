<div align="center">
<img src="assets/icon.png" width="96" height="96" alt="Nexus.ssh icon">

# Nexus.ssh

**A fast, modern SSH, SFTP, and RDP client for Windows and Linux — free.**

[![Download for Windows](https://img.shields.io/badge/Download-Windows-4f8ef7?style=for-the-badge&logo=windows&logoColor=white)](../../releases/latest)
[![Download for Linux](https://img.shields.io/badge/Download-Linux-4f8ef7?style=for-the-badge&logo=linux&logoColor=white)](../../releases/latest)
[![Support on Ko-fi](https://img.shields.io/badge/Support-Ko--fi-ff5e5b?style=for-the-badge&logo=ko-fi&logoColor=white)](https://ko-fi.com/vladyslavdubov)

</div>

---

## What it is

Nexus.ssh is a desktop terminal for people who spend their day connected to
remote servers. One app for SSH sessions, SFTP file browsing, and full RDP
remote desktop — no juggling three different tools, no subscription.

- 🖥️ **SSH terminal** — tabs, session folders, saved connections
- 📁 **SFTP browser** — drag-and-drop uploads, a built-in file editor, and
  elevated (sudo) file access when you need it
- 🖱️ **RDP built in** — a native remote desktop client, no separate download
- 🔑 **Encrypted key vault** — SSH keys and credentials, encrypted at rest,
  never stored in plaintext
- ⚡ **Multi-Exec** — run one command or script across many hosts at once
- 📊 **Dashboard** — live CPU/RAM/disk monitoring across your fleet
- 🤖 **AI assistant** — in-app chat that understands your SSH context
- 🆓 **Completely free** — every feature, no paywalls, no trial

## Download

Grab the latest build from the **[Releases page](../../releases/latest)**.

### Windows

| File | Use this if... |
|---|---|
| `Nexus.ssh_x64-setup.exe` | You just want to install it (recommended) |
| `Nexus.ssh_x64.msi` | Your organization deploys software via MSI |

**Requirements:** Windows 10 (64-bit) or newer.

#### About the security warning

Nexus.ssh is a small independent project without a paid code-signing
certificate yet, so Windows SmartScreen will show an **"Windows protected
your PC"** warning the first time you run the installer. This is normal for
unsigned software, not a sign anything is wrong. Click **More info → Run
anyway** to continue.

### Linux

| File | Use this if... |
|---|---|
| `Nexus.ssh_amd64.deb` | Debian, Ubuntu, Mint, Pop!\_OS, or any `apt`-based distro |
| `Nexus.ssh-1.x86_64.rpm` | Fedora, RHEL, openSUSE, or any `rpm`-based distro |
| `Nexus.ssh_amd64.AppImage` | Any other distro, or if you don't want to install anything system-wide |

**Requirements:** a 64-bit distro with `webkit2gtk` available (present by
default on most modern desktop distros).

Install with your package manager:

```bash
# Debian / Ubuntu / Mint
sudo apt install ./Nexus.ssh_*_amd64.deb

# Fedora / RHEL / openSUSE
sudo rpm -i Nexus.ssh-*.x86_64.rpm
# or: sudo dnf install ./Nexus.ssh-*.x86_64.rpm
```

For the AppImage, no installation is needed — just make it executable and run it:

```bash
chmod +x Nexus.ssh_*_amd64.AppImage
./Nexus.ssh_*_amd64.AppImage
```

If it won't launch and mentions FUSE, install `libfuse2` (older distros) or
run it with `--appimage-extract-and-run`.

## Support the project

Nexus.ssh is free with no catch — no ads, no telemetry you didn't opt into,
no feature paywalls. If it's useful to you, consider supporting continued
development:

**[☕ ko-fi.com/vladyslavdubov](https://ko-fi.com/vladyslavdubov)**

## Found a bug?

Open an [issue](../../issues) — screenshots and steps to reproduce help a
lot. Please don't include real hostnames, IPs, or credentials in bug
reports/screenshots.

## Privacy

Your saved sessions, SSH keys, and credentials are encrypted at rest on your
own machine and never leave it except to connect to the servers you tell it
to. Crash reporting is opt-in and off by default; when enabled, it only ever
sends a stack trace, app version, and OS — never session content, hostnames,
or credentials.

---

<div align="center">
<sub>This repository hosts pre-built installers only. Built with Tauri + Rust + React.</sub>
</div>
