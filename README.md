# Debian Linux on Microsoft Surface Pro

![Debian](https://img.shields.io/badge/Debian-A81D33?style=flat&logo=debian&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![Microsoft Surface](https://img.shields.io/badge/Microsoft%20Surface-0078D4?style=flat&logo=microsoft&logoColor=white)

> A practical troubleshooting log for reviving an old Surface Pro with Debian, and the issues you will likely run into along the way.

---

## Overview

There are plenty of videos and guides on installing **any** Linux distro on an older Surface Pro. I tried many of them myself. After running into a handful of issues, I would usually give up for weeks, then try again on a different distro. The troubleshooting process was tedious, but I eventually got it working.

This repository documents what I learned and aims to add more insight into the common problems on this never-ending quest to revive old hardware.

---

## Getting Started

Begin with the installation steps from one of the following guides:

| Resource | Description |
|----------|-------------|
| [linux-surface/linux-surface](https://github.com/linux-surface/linux-surface) | The official project for Linux kernel and driver support on Surface devices |
| [Low-Cost Linux: Re-purposing a Microsoft Surface Pro Tablet](https://community.element14.com/technologies/test-and-measurement/b/blog/posts/low-cost-linux-re-purposing-a-microsoft-surface-pro-tablet) | A step-by-step walkthrough on element14 |

> [!IMPORTANT]
> I know how this sounds, but **you will probably need to make a mistake first**. Only then will you reach the solution. The sections below are meant to shorten that process.

---

## Prerequisites

- A Microsoft Surface Pro (older generation)
- A USB flash drive (8 GB or larger)
- A Debian ISO ([download here](https://www.debian.org/distrib/))
- A USB hub or adapter for a keyboard and mouse during setup
- A stable internet connection

---

## Installation

1. Follow the installation steps from one of the guides above.
2. Boot from the USB drive.
3. Install Debian.
4. Add the `linux-surface` kernel and drivers once Debian is running.

```bash
# Example: update the system after the first boot
sudo apt update && sudo apt full-upgrade -y
```

---

## Troubleshooting

> Add each issue you hit below, along with the fix that worked.

### Issue 1: `<short description>`

**Symptom:**

```text
<error message or behavior>
```

**Fix:**

```bash
# commands that resolved it
```

### Issue 2: `<short description>`

**Symptom:** ...

**Fix:** ...

---

## Contributing

Found another issue or a better fix? Contributions are welcome.

1. Fork this repository
2. Create a branch: `git checkout -b fix/your-issue`
3. Commit your changes: `git commit -m "Add fix for ..."`
4. Push the branch: `git push origin fix/your-issue`
5. Open a pull request

---

## Acknowledgments

- [linux-surface](https://github.com/linux-surface/linux-surface) contributors
- The element14 community

---

## License

Distributed under the MIT License. See `LICENSE` for details.
