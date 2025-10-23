# Understanding Linux — A Step-by-Step Guide for Beginners

A concise, practical introduction to Linux: what it is, a short history, essential commands, filesystem layout, exercises, tips, and resources.

## Table of contents
- [What is Linux?](#what-is-linux)
- [Brief history](#brief-history)
- [Why learn Linux?](#why-learn-linux)
- [Common commands](#common-commands)
    - [Navigating the filesystem](#navigating-the-filesystem)
    - [File operations](#file-operations)
    - [Process management](#process-management)
    - [Permissions & ownership](#permissions--ownership)
- [Filesystem hierarchy](#filesystem-hierarchy)
- [Exercises](#exercises)
- [Tips](#tips)
- [Resources](#resources)
- [Popular Linux Distributions](#popular-linux-distributions)

---

## What is Linux?
Linux is an open-source family of operating systems built around the Linux kernel (first released by Linus Torvalds in 1991). Many distributions (Ubuntu, Fedora, CentOS, etc.) package the kernel with tools and userland software.

## Brief history
- **1969** — Unix developed at AT&T Bell Labs (precursor concepts).  
- **1983** — GNU Project started to create a free Unix-like OS.  
- **1991** — Linus Torvalds released the Linux kernel.  
- **1992** — Linux became widely available as open source.  
- **2000s+** — Linux grows in servers, embedded systems, cloud, and desktops.

## Why learn Linux?
- Open source — free to inspect and modify.  
- Versatile — runs on servers, desktops, mobile devices, and embedded hardware.  
- Strong community — abundant documentation and community support.  
- Valuable skill — common in development, operations, and cloud environments.

## Common commands

### Navigating the filesystem
- `ls` — list files and directories  
- `cd` — change directory  
- `pwd` — print working directory  
- `mkdir` — create a directory  
- `rm` — remove files or directories

Example:
```bash
ls -la
cd ~/projects
pwd
mkdir new-folder
rm old-file.txt
```

### File operations
- `cp` — copy files or directories  
- `mv` — move or rename files  
- `cat` — display file contents  
- `nano`, `vim` — edit files

Example:
```bash
cp file.txt file.backup
mv draft.md final.md
cat README.md
nano notes.txt
```

### Process management
- `ps` — show running processes  
- `top` / `htop` — monitor system resources  
- `kill` — terminate a process

Example:
```bash
ps aux | grep myapp
top
kill 12345
```

### Permissions & ownership
- `chmod` — change file permissions  
- `chown` — change file owner/group  
- `sudo` — run commands as superuser

Quick examples:
```bash
chmod +x script.sh
sudo chown user:group /var/www
sudo apt update
```

## Filesystem hierarchy
- `/` — root directory  
- `/home` — user home directories  
- `/etc` — system configuration files  
- `/var` — variable data (logs, caches)  
- `/usr` — user-installed software and libraries  
- `/tmp` — temporary files

## Exercises
1. Navigate to your home and create a folder:
     ```bash
     cd ~
     mkdir practice-linux
     ```
2. Create a text file, add content, and display it:
     ```bash
     echo "Hello Linux" > practice-linux/hello.txt
     cat practice-linux/hello.txt
     ```
3. Make a script executable and run it:
     ```bash
     echo -e "#!/bin/bash\n echo Hello" > practice-linux/run.sh
     chmod +x practice-linux/run.sh
     ./practice-linux/run.sh
     ```

## Tips
- Use `man <command>` for the manual (e.g., `man ls`).  
- Practice in a VM, container, WSL, or cloud instance to avoid harming your main system.  
- Start with a beginner-friendly distro (Ubuntu, Fedora) and explore shells like Bash or Zsh.

## Resources
- https://linuxjourney.com/ — interactive lessons  
- https://linuxcommand.org/ — The Linux Command Line book and tutorials  
- https://www.gnu.org/ — GNU Project and related resources

## Popular Linux Distributions

Linux distributions (distros) package the Linux kernel with tools, libraries, and user interfaces. Here are some popular ones:

### Ubuntu
- **Target Audience**: Beginners and general users.
- **Features**: User-friendly, large community, and extensive documentation.
- **Use Cases**: Desktops, servers, and cloud environments.
- **Package Manager**: `apt` (Advanced Package Tool).
- **Website**: [https://ubuntu.com](https://ubuntu.com)

### Fedora
- **Target Audience**: Developers and tech enthusiasts.
- **Features**: Cutting-edge software, frequent updates, and a focus on open-source.
- **Use Cases**: Development workstations and testing environments.
- **Package Manager**: `dnf` (Dandified YUM).
- **Website**: [https://getfedora.org](https://getfedora.org)

### CentOS
- **Target Audience**: Enterprises and server administrators.
- **Features**: Stability, long-term support, and compatibility with Red Hat Enterprise Linux (RHEL).
- **Use Cases**: Servers and production environments.
- **Package Manager**: `yum`/`dnf`.
- **Website**: [https://www.centos.org](https://www.centos.org)

### Debian
- **Target Audience**: Advanced users and developers.
- **Features**: Stability, large repository of packages, and a strong focus on free software.
- **Use Cases**: Servers, desktops, and embedded systems.
- **Package Manager**: `apt`.
- **Website**: [https://www.debian.org](https://www.debian.org)

### Arch Linux
- **Target Audience**: Advanced users who prefer customization.
- **Features**: Minimalist, rolling release, and a "do-it-yourself" philosophy.
- **Use Cases**: Custom setups and learning Linux internals.
- **Package Manager**: `pacman`.
- **Website**: [https://archlinux.org](https://archlinux.org)

### OpenSUSE
- **Target Audience**: Developers and system administrators.
- **Features**: Stability, YaST configuration tool, and enterprise-grade options.
- **Use Cases**: Desktops, servers, and development environments.
- **Package Manager**: `zypper`.
- **Website**: [https://www.opensuse.org](https://www.opensuse.org)

### Linux Mint
- **Target Audience**: Beginners and users transitioning from Windows.
- **Features**: User-friendly, pre-installed codecs, and a Windows-like interface.
- **Use Cases**: Desktops and laptops.
- **Package Manager**: `apt`.
- **Website**: [https://linuxmint.com](https://linuxmint.com)

### Red Hat Enterprise Linux (RHEL)
- **Target Audience**: Enterprises and professionals.
- **Features**: Commercial support, security, and stability.
- **Use Cases**: Servers, cloud, and enterprise applications.
- **Package Manager**: `yum`/`dnf`.
- **Website**: [https://www.redhat.com](https://www.redhat.com)

---

Each distribution has its strengths and is tailored for specific use cases. Beginners often start with Ubuntu or Linux Mint, while advanced users explore Arch Linux or Debian.

Stay curious and practice regularly — small daily tasks build strong CLI fluency.