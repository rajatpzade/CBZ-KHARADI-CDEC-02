# Day-6



## Mastering the Linux File System Hierarchy

### Mastering the Linux File System — 19 important directories

- / (root)
  - The top of the filesystem tree. All paths start here.
  - Example: ls -ld /

- /bin
  - Essential user binaries (commands) required for single-user mode and for all users (ls, cp, mv).
  - Example: ls -l /bin/ls

- /boot
  - Files required to boot the system: kernel, initramfs, bootloader config.
  - Example: ls -l /boot

- /dev
  - Device files representing hardware and virtual devices (e.g., /dev/sda).
  - Example: ls -l /dev/sda*

- /etc
  - System-wide configuration files and startup scripts.
  - Example: ls -la /etc | head

- /home
  - Users' personal directories (e.g., /home/rajat).
  - Example: ls -la /home

- /lib
  - Shared libraries required by binaries in /bin and /sbin (32-bit systems).
  - Example: ls -l /lib | head

- /lib64
  - 64-bit shared libraries on 64-bit systems.
  - Example: ls -l /lib64 | head

- /media
  - Mount points for removable media (USB CDs) created automatically (GUI systems).
  - Example: ls -la /media

- /mnt
  - Temporary mount point for administrators (manual mounts).
  - Example: sudo mount /dev/sdb1 /mnt; ls /mnt

- /opt
  - Optional add-on application packages (third-party software).
  - Example: ls -l /opt

- /proc
  - Virtual filesystem providing process and kernel information (procfs).
  - Example: cat /proc/cpuinfo

- /root
  - Home directory for the root user (not the same as /).
  - Example: ls -la /root

- /run
  - Runtime data since boot (sockets, pids); volatile.
  - Example: ls -la /run

- /sbin
  - System binaries for administration (fdisk, ifconfig) — usually run by root.
  - Example: ls -l /sbin

- /srv
  - Data for services provided by the system (WWW, FTP data).
  - Example: ls -la /srv

- /sys
  - Virtual filesystem exposing kernel objects and device tree (sysfs).
  - Example: ls -la /sys/class/net

- /tmp
  - Temporary files — world-writable, often cleared at reboot.
  - Example: ls -la /tmp

- /var
  - Variable data: logs (/var/log), mail, spool files, package caches.
  - Example: ls -la /var/log

---

## The Significance of the Linux File System Hierarchy

- Predictability: standard locations make it easy to find binaries, configs, and logs.
- Separation of concerns: isolates user data, system files, runtime data, and optional software.
- Permissions & security: directories have differing default permissions and purposes.
- Maintainability: backups, package management, and recovery are simpler with a consistent layout.

---

## Inside the Linux Root Directory: What You Need to Know

- Root (/) contains mount points and top-level directories — do not store user files directly in /.
- Mounted filesystems (external disks, network mounts) appear at mount points (e.g., /mnt, /media).
- Virtual filesystems (/proc, /sys, /run) are kernel-provided views — read-only or volatile.
- Lost+found: usually present on filesystems formatted with ext{2,3,4}; stores recovered file fragments after fsck.
- Use ls -ld and stat to inspect ownership, perms, and mount points:
  - stat /

---

## Understanding the Functionality of Common Linux Directories (quick guide)

- Binaries: /bin, /sbin, /usr/bin, /usr/sbin
  - User vs system admin tools; /usr/* holds larger collections installed by packages.
- Libraries: /lib, /lib64, /usr/lib
  - Shared code used by binaries.
- Configuration: /etc
  - Centralized system configuration; backup before editing.
- User data: /home, /root
  - Personal files and settings per user.
- Variable & logs: /var (logs, spools, caches)
  - Monitor /var/log for troubleshooting.
- Boot & kernel: /boot
  - Kernel images and bootloader files.
- Devices & runtime: /dev, /proc, /sys, /run
  - Device nodes, process info, kernel object interfaces, and runtime state.
- Optional & service data: /opt, /srv
  - Third-party apps and service-specific content.
- Temporary: /tmp
  - Short-lived files; safe to clean periodically.

---

## Introduction to Linux Shortcuts: Boost Your Efficiency

- ~ (tilde)
  - Shortcut for current user's home directory.
  - Example: cd ~ or cd ~/projects

- / (root)
  - Absolute path starts at root: cd /etc

- . (dot)
  - Current directory. Useful in commands: ./script.sh

- .. (double dot)
  - Parent directory. Example: cd ..

- - (dash)
  - Previous directory. Example: cd -  (switch back)

- Tab completion
  - Press Tab to auto-complete commands, filenames, and paths.

- Ctrl+R (reverse search)
  - Interactive history search to find previous commands.

- Ctrl+C and Ctrl+Z
  - Ctrl+C: kill running foreground process.
  - Ctrl+Z: suspend process (use bg/fg to resume).

- pushd / popd / dirs
  - Directory stack for quick navigation.
  - Example: pushd /var/log; popd

- Aliases
  - Short commands: alias ll='ls -lah'
  - Add to ~/.bashrc to persist.

- Symbolic links
  - Create shortcuts inside filesystem: ln -s /path/to/target ~/shortcut

---

## Hands-on Exercises (short)

1. List top-level directories and permissions:
   - ls -la /
2. Check mount points and disks:
   - lsblk; mount | grep '^/dev'
3. Inspect kernel and process info:
   - cat /proc/cpuinfo | head
4. Use shortcuts:
   - cd ~; mkdir -p ~/lab; pushd /var/log; popd; cd -
5. Create an alias and persist it:
   - echo "alias ll='ls -lah'" >> ~/.bashrc; source ~/.bashrc

---

## Quick Reference (commands)

- Inspect directories:
  - ls -la /path
  - stat /path
- Disk & mounts:
  - lsblk
  - df -h
  - mount
- Virtual fs:
  - ls /proc
  - ls /sys
- Links:
  - ln -s /target /link
- Shortcuts:
  - cd ~, cd -, cd .., Tab, Ctrl+R