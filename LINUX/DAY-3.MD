## Getting Started with Operating Systems

### What is an Operating System (OS)?
- Software that manages computer hardware and provides services to applications and users.
- Acts as an intermediary between user programs and physical hardware.

### Main Responsibilities
- Process management (create, schedule, terminate processes)
- Memory management (allocate/free RAM)
- File system management (read/write, permissions)
- Device management (drivers for hardware)
- Security and access control
- User interface (CLI/GUI)

---

## Different Types of Operating Systems
- Batch OS — Executes jobs in batches (old mainframes).
- Time-Sharing / Multiuser — Many users share CPU time (e.g., Unix).
- Real-Time OS — Deterministic response for embedded systems.
- Distributed OS — Manages distributed resources across networked machines.
- Network OS — Provides network services (file/print sharing).
- Mobile OS — Optimized for phones/tablets (Android, iOS).
- Embedded OS — For appliances and IoT devices (RTOS, Embedded Linux).

---

## How Operating Systems Impact Your Daily Life
- Enable running apps (browsers, email, messaging).
- Manage smartphone operations (calls, notifications, apps).
- Provide security (user accounts, permissions, updates).
- Control home devices (routers, smart TVs) via embedded OS.
- Power cloud servers and web services people use daily.

---

## Windows vs Unix vs Linux

### Ownership and Origin
- Windows: Developed by Microsoft; proprietary.
- Unix: Originated at AT&T Bell Labs (1970s); many commercial variants (AIX, HP-UX).
- Linux: Kernel by Linus Torvalds (1991); open-source, many distributions (Ubuntu, CentOS).

### Cost and Licensing
- Windows: Commercial license; paid for many editions.
- Unix: Commercial licensing for most proprietary flavors.
- Linux: Mostly free/open-source (GPL); some enterprise distributions offer paid support.

### Security and Privacy
- Windows: Larger target for malware; frequent security updates; telemetry in some editions.
- Unix: Historically used in servers; strong POSIX security model.
- Linux: Strong permission model; active patching and community audits; customizable privacy.

### User Interface
- Windows: Graphical, user-friendly GUI; consistent UX.
- Unix: Historically CLI-first; GUIs available (X11, Wayland).
- Linux: Flexible — CLI (bash, zsh) and multiple desktop environments (GNOME, KDE).

---

## What is a Server?
- A server is a computer or program that provides services to other computers (clients) over a network.
- Examples: web server (Apache, Nginx), database server (MySQL, PostgreSQL), file server (Samba).

---

## Desktop OS vs Server OS

Desktop OS
- Optimized for interactive user experience (GUI, multimedia, peripherals).
- Examples: Windows Desktop, macOS, Ubuntu Desktop.
- Focus: user applications, responsiveness.

Server OS
- Optimized for reliability, performance, remote access and headless operation.
- Examples: Windows Server, Ubuntu Server, CentOS, RHEL.
- Focus: network services, concurrency, uptime, security.

Key differences
- GUI presence (server often headless), default services, update cadence, tuning for workloads.

---

## Introduction to Linux
- Linux refers to the kernel; common distributions bundle the kernel with GNU tools and packages.
- Popular distros: Ubuntu, Debian, Fedora, CentOS, Arch.
- Strengths: open-source, flexible, strong server adoption, container & cloud friendly.

Quick commands for students:
- Check kernel and OS:
  - uname -a
  - lsb_release -a  (may require lsb-release package)
- List processes:
  - ps aux | head
  - top or htop
- Disk and filesystems:
  - lsblk
  - df -h

---

## Architecture of Linux — Layered Notes

- Hardware
  - Physical components: CPU, RAM, disk, network cards, peripherals.
  - Provides raw resources that the kernel manages.

- Kernel
  - Core of the OS: device drivers, process scheduler, memory manager, filesystem (VFS), network stack.
  - Exposes system calls as the interface for user-space programs.
  - Runs in kernel space with full hardware access.

- Shell
  - Command-line interface that interprets user commands and scripts (examples: bash, zsh).
  - Acts as a bridge between the user and kernel (invokes system calls, launches processes).
  - Can be used interactively or for automation via scripts.

- Application
  - User-space programs (browsers, editors, daemons, services).
  - Run with limited privileges and use system calls to request kernel services.
  - Isolated from kernel space to protect system stability and security.

- User (User Layer)
  - Humans and user accounts interacting with the system via shell or GUI.
  - Owns and runs applications; subject to permission and access control enforced by kernel.
  - Includes desktop environments and user sessions.

Diagram (simple)
- Hardware ←→ Kernel (drivers, scheduler, memory) ←→ System Calls ←→ User Space (shells, services, apps)

![Alt Text](img/Linux_arch.png)

---

## Simple Learning Exercises
1. Identify your OS:
   - uname -a
   - lsb_release -a
2. Create a file and check permissions:
   - touch ~/testfile && ls -l ~/testfile
3. View running services:
   - systemctl list-units --type=service | head
4. Explore processes:
   - ps aux --sort=-%cpu | head

---

## Quick Summary for Students
- OS manages hardware and provides a platform for apps.
- Types of OS vary by purpose (desktop, server, real-time, embedded).
- Linux is open-source, widely used on servers and in cloud environments.
- Understanding kernel, system calls, filesystem, and user space is key to Linux mastery.
