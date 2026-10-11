# Debian Linux on Microsoft Surface Pro

![Debian](https://img.shields.io/badge/Debian-A81D33?style=flat&logo=debian&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![Microsoft Surface](https://img.shields.io/badge/Microsoft%20Surface-0078D4?style=flat&logo=microsoft&logoColor=white)

> A practical troubleshooting log for reviving an old Surface Pro with Linux, and the issues you will likely run into along the way.

---

## Overview

There are plenty of videos and guides on installing **any** Linux distro on an older Surface Pro. I tried many of them myself. After running into a handful of issues, I would usually give up for weeks, then try again on a different distro. The troubleshooting process was tedious, but I eventually got it working.

This repository documents what I learned and aims to add more insight into the common problems on this never-ending quest to revive old hardware.

---

## My Setup

| Component | Spec |
|-----------|------|
| **Device** | Microsoft Surface Pro (Model 1796) |
| **RAM** | 4 GB |
| **CPU** | Intel Core i5, 7th generation |
| **OS** | Ultramarine Linux with KDE Plasma |

---

## Getting Started

Begin with the installation steps from one of the following guides:

| Resource | Description |
|----------|-------------|
| [linux-surface/linux-surface](https://github.com/linux-surface/linux-surface) | The official project for Linux kernel and driver support on Surface devices |
| [Low-Cost Linux: Re-purposing a Microsoft Surface Pro Tablet](https://community.element14.com/technologies/test-and-measurement/b/blog/posts/low-cost-linux-re-purposing-a-microsoft-surface-pro-tablet) | A step-by-step walkthrough on element14 |

> [!IMPORTANT]
> I know how this sounds, but **you will probably need to make a mistake first**. Only then will you reach the solution. The section [Steps to Actually Fix the Issue](#steps-to-actually-fix-the-issue) is meant to shorten that process.

---

## Prerequisites

- A Microsoft Surface Pro (older generation)
- A USB flash drive (8 GB or larger)
- An ISO image of your chosen distro
- A USB hub or adapter for a keyboard and mouse during setup
- A stable internet connection

---

## Installation

1. Follow the installation steps from one of the guides above.
2. Boot from the USB drive.
3. Install your Debian distro.
4. Add the `linux-surface` kernel and drivers once your system is running. If this step fails, see [Steps to Actually Fix the Issue](#steps-to-actually-fix-the-issue).

```bash
# Example: update the system after the first boot
sudo apt update && sudo apt full-upgrade -y
```

---

## Steps to Actually Fix the Issue

### Problem: `Usable URL not found` for `kernel-surface`

**Symptom:** Running the install command fails with an error like this:

```text
Usable URL not found
```

```bash
sudo dnf install kernel-surface iptsd
```

**Cause:** The `linux-surface` repository config uses a dynamic variable (`$releasever`) to build the package URL. If you are on a newer Fedora-based release (for example, Fedora 44) and the maintainers have not published packages for it yet, that folder does not exist on their servers. DNF requests it, receives a `404 Not Found`, and gives up.

**Fix:** Point the repository at the last release that has working packages (for example, Fedora 43).

#### 1. Rewrite the repository configuration

Open the repo file in a terminal editor:

```bash
sudo nano /etc/yum.repos.d/linux-surface.repo
```

Replace its contents with the following:

```ini
[linux-surface]
name=linux-surface
baseurl=https://pkg.surfacelinux.com/fedora/f43/
enabled=1
skip_if_unavailable=1
gpgkey=https://raw.githubusercontent.com/linux-surface/linux-surface/master/pkg/keys/surface.asc
gpgcheck=1
enabled_metadata=1
type=rpm-md
repo_gpgcheck=0
```

Press `CTRL+O`, then `Enter` to save, and `CTRL+X` to exit nano.

#### 2. Clear the DNF cache

```bash
sudo dnf clean all
```

#### 3. Install the Surface kernel and touch driver

```bash
sudo dnf install kernel-surface iptsd
```

> [!WARNING]
> Do **not** include `libwacom-surface` for now. It conflicts heavily with modern Fedora versions and will break the installation.

#### 4. Disable Secure Boot and TPM, then reboot

1. Shut down the Surface.
2. Make sure **Secure Boot** and **TPM** are disabled.
3. Power the Surface back on normally.

---

## Acknowledgments

- [linux-surface](https://github.com/linux-surface/linux-surface) contributors
- The element14 community

---

## License

Distributed under the MIT License. See `LICENSE` for details.
