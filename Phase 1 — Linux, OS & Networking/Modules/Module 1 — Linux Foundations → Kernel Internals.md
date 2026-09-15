
# Module 1 — Linux Foundations → Kernel Internals
> Part of: DevOps Mastery Roadmap — Phase 1 (Linux + OS + Networking)
> Learning mode: Basic → Intermediate → Advanced, in one continuous ladder
> Tags: **[OS]** = Operating Systems theory · **[CN]** = Networking · **[SEC]** = Security · **[PERF]** = Performance
 
---
 
## 0. How to use this file
This is a **topic map**, not a tutorial. For every leaf node:
1. Learn the concept (article/video/docs).
2. Run the related command(s) yourself on a real Linux box/VM.
3. Write one line in your own words explaining "why this exists."
4. Check it off.
---
 
## 1. Mindmap Overview
 
```
MODULE 1: LINUX FOUNDATIONS → KERNEL INTERNALS
│
├── 1. Linux Landscape
│   ├── History & Philosophy (Unix lineage, GNU/Linux, open source model)
│   ├── Distro Families
│   │   ├── Debian-based (Ubuntu, Debian, Mint) — apt/dpkg
│   │   ├── RHEL-based (RHEL, CentOS, Fedora, Rocky, Alma) — yum/dnf/rpm
│   │   └── Others (Arch/pacman, SUSE/zypper) — awareness only
│   └── Choosing a distro for server vs desktop use
│
├── 2. System Architecture Layers
│   ├── Hardware
│   ├── Kernel Space           [OS]
│   ├── System Call Interface  [OS]
│   ├── Userspace / Shell
│   └── Applications
│
├── 3. The Boot Process                         [OS: bootstrapping]
│   ├── Firmware stage
│   │   ├── BIOS (legacy)
│   │   └── UEFI (modern, Secure Boot)
│   ├── Bootloader stage
│   │   ├── GRUB2 basics
│   │   ├── GRUB config files (/etc/default/grub, grub.cfg)
│   │   └── Kernel selection / boot parameters
│   ├── Kernel initialization
│   │   ├── initramfs / initrd (temporary root filesystem)
│   │   ├── Kernel decompression & hardware detection
│   │   └── Mounting the real root filesystem
│   └── Init system takeover
│       ├── systemd (modern default)
│       ├── SysVinit (legacy, for context)
│       └── Runlevels vs systemd targets
│
├── 4. Filesystem Hierarchy Standard (FHS)
│   ├── /bin, /sbin — essential binaries
│   ├── /etc — configuration files
│   ├── /home — user directories
│   ├── /var — variable data (logs, spool, cache)
│   ├── /usr — user programs & libraries
│   ├── /tmp — temporary files
│   ├── /opt — optional/third-party software
│   ├── /proc — virtual filesystem, live kernel/process data     [OS]
│   ├── /sys — virtual filesystem, kernel device/driver data     [OS]
│   ├── /dev — device files (block & character devices)
│   └── /lib, /lib64 — shared libraries
│
├── 5. Navigation & File Operations
│   ├── Navigation: pwd, cd, ls (flags: -l, -a, -h, -R)
│   ├── Search: find, locate, updatedb, which, whereis
│   ├── File ops: cp, mv, rm, mkdir, rmdir, touch
│   ├── Links
│   │   ├── Hard links — same inode, same data          [OS: inodes]
│   │   └── Symbolic (soft) links — pointer to a path
│   └── Viewing/Editing
│       ├── cat, tac, head, tail, tail -f
│       ├── less vs more (pager internals)
│       └── vim (modes: normal/insert/visual, basic motions, :wq, search/replace)
│
├── 6. Package Management
│   ├── Debian family
│   │   ├── apt (high-level: install/remove/update/upgrade)
│   │   └── dpkg (low-level: .deb handling)
│   ├── RHEL family
│   │   ├── dnf/yum (high-level)
│   │   └── rpm (low-level: .rpm handling)
│   ├── Dependency resolution concept
│   ├── Repositories & GPG signing of packages           [SEC]
│   └── Building/compiling from source (./configure, make, make install)
│
├── 7. systemd Deep Dive
│   ├── Unit types: .service, .socket, .timer, .target, .mount
│   ├── systemctl: start/stop/enable/disable/status/restart
│   ├── journalctl: log querying, filtering by unit/time/priority
│   ├── Writing a custom .service file
│   │   ├── [Unit] section (Description, After, Requires)
│   │   ├── [Service] section (ExecStart, Restart, User)
│   │   └── [Install] section (WantedBy)
│   ├── Targets vs old runlevels (multi-user.target, graphical.target)
│   └── systemd timers vs cron (modern alternative to crontab)
│
├── 8. Kernel Interfaces to Userspace              [OS]
│   ├── /proc filesystem
│   │   ├── /proc/cpuinfo, /proc/meminfo, /proc/version
│   │   ├── /proc/<pid>/ — per-process live data (status, fd, maps)
│   │   └── /proc/sys — tunable kernel parameters (sysctl-backed)
│   ├── /sys filesystem
│   │   ├── Device and driver hierarchy
│   │   └── Kernel object model exposure
│   └── sysctl — reading & modifying kernel parameters at runtime
│
├── 9. System Call Interface                        [OS: syscall interface, mode switching]
│   ├── What a syscall is — user mode → kernel mode transition
│   ├── Common syscall categories
│   │   ├── Process control (fork, exec, exit, wait)
│   │   ├── File management (open, read, write, close)
│   │   ├── Device management (ioctl)
│   │   └── Information maintenance (getpid, alarm)
│   ├── Tracing tools
│   │   ├── strace — trace syscalls of a running/new process
│   │   └── ltrace — trace library calls
│   └── Reading strace output: understanding syscall return values & errno
│
├── 10. Kernel Modules                              [OS: kernel extensibility]
│   ├── Monolithic kernel with loadable modules (Linux's actual model)
│   ├── lsmod — list loaded modules
│   ├── modprobe / insmod / rmmod — load/unload modules
│   ├── modinfo — inspect a module
│   └── (Optional deep dive) writing a minimal "Hello World" kernel module
│
└── 11. Module 1 Capstone Checkpoint
    ├── Task: Fresh Linux VM — narrate the entire boot process from power-on to login prompt using journalctl -b
    ├── Task: Use strace on a simple command (e.g. `ls`) and identify at least 5 distinct syscalls
    ├── Task: Write a custom systemd .service that runs a script on boot and restarts on failure
    └── Task: Explore /proc/<your-shell-pid>/ and explain 5 files found inside it
```
 
---
 
## 2. Detailed Topic Table (Basic → Intermediate → Advanced)
 
| # | Topic | Level | Tag | Key Commands / Files |
|---|-------|-------|-----|----------------------|
| 1 | Linux history, GNU/Linux, distro families | Basic | — | `cat /etc/os-release` |
| 2 | Kernel vs userspace vs shell | Basic | [OS] | — |
| 3 | FHS: /etc, /var, /home, /tmp, /usr, /opt | Basic | [OS] | `ls /` |
| 4 | Navigation & file ops | Basic | — | `ls, cd, cp, mv, rm, find` |
| 5 | Hard vs soft links & inodes | Basic/Intermediate | [OS] | `ln, ln -s, ls -i` |
| 6 | vim basics | Basic | — | `vim` |
| 7 | Package managers (apt/dnf) high-level | Basic | — | `apt install/remove/update` |
| 8 | Package managers low-level (dpkg/rpm) | Intermediate | — | `dpkg -i, rpm -ivh` |
| 9 | Repository & GPG package signing | Intermediate | [SEC] | `apt-key`, `/etc/apt/sources.list` |
| 10 | Compiling from source | Intermediate | — | `./configure && make && make install` |
| 11 | systemd unit basics & systemctl | Intermediate | [OS] | `systemctl status/start/enable` |
| 12 | journalctl log querying | Intermediate | — | `journalctl -u, -b, -p` |
| 13 | Writing custom .service files | Intermediate/Advanced | [OS] | `/etc/systemd/system/*.service` |
| 14 | systemd timers vs cron | Intermediate | — | `systemctl list-timers` |
| 15 | Boot process: firmware → GRUB → initramfs → systemd | Advanced | [OS: bootstrapping] | `journalctl -b`, `/boot/grub/grub.cfg` |
| 16 | /proc and /sys as kernel interfaces | Advanced | [OS] | `cat /proc/meminfo`, `ls /sys/class` |
| 17 | sysctl runtime kernel tuning | Advanced | [OS][PERF] | `sysctl -a`, `/etc/sysctl.conf` |
| 18 | Syscall interface & mode switching | Advanced | [OS: syscall interface] | conceptual |
| 19 | strace / ltrace tracing | Advanced | [OS] | `strace -f -e trace=open ls` |
| 20 | Kernel modules: lsmod/modprobe/insmod | Advanced | [OS: extensibility] | `lsmod, modprobe, modinfo` |
 
---
 
## 3. Concept Deep-Dive Notes (fill in as you learn)
 
### 3.1 Boot Process
- [ ] What happens in the first 2 seconds of powering on a Linux server?
- [ ] Why does the kernel need an initramfs before mounting the real root filesystem?
- [ ] Difference between a systemd *target* and an old SysVinit *runlevel*?
### 3.2 Kernel/Userspace Boundary
- [ ] Why can't userspace code directly touch hardware?
- [ ] What triggers a mode switch from user mode to kernel mode?
- [ ] Where does a syscall number get resolved to actual kernel code?
### 3.3 /proc and /sys
- [ ] Name 5 files under `/proc/<pid>/` and what each reveals.
- [ ] Difference in purpose between `/proc` (process/kernel state) and `/sys` (device/driver model).
### 3.4 Kernel Modules
- [ ] Why is Linux called a "monolithic kernel with loadable modules" rather than a true microkernel?
- [ ] What's the risk of loading an untrusted kernel module? **[SEC]**
---
 
## 4. Capstone Checklist
- [ ] Narrated full boot sequence using `journalctl -b` on a real VM
- [ ] Traced ≥5 syscalls of a simple command with `strace`
- [ ] Wrote and deployed a custom `.service` unit (starts on boot, restarts on failure)
- [ ] Explored and explained 5 files inside `/proc/<pid>/`
- [ ] One-paragraph summary, in your own words: "How does a Linux system go from powered-off to a running shell prompt, and where does the kernel take over from firmware?"
---
 
## 5. Portability Note
This file is self-contained and reusable: paste/upload it into any fresh Claude conversation and ask Claude to "teach me Module 1 from this file, one section at a time" to reproduce this exact curriculum and get consistent teaching regardless of prior chat history.
