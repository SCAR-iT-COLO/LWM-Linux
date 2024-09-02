# Linux System Recovery

## 1. Assess the Problem
First, determine the nature of the issue:
- Boot failure
- File system corruption
- Broken package dependencies
- Kernel panic
- Forgotten root password

## 2. Boot into Recovery Mode
Most Linux distributions offer a recovery mode:
- Restart your system
- Press and hold Shift (for GRUB2) during boot
- Select "Advanced options" then "Recovery mode"

## 3. Check File System Integrity
Use fsck (file system check) utility:
```
fsck /dev/sdXY
```
Replace X with the drive letter and Y with the partition number.

## 4. Mount File Systems
If necessary, remount the root file system as read-write:
```
mount -o remount,rw /
```

## 5. Network Connectivity
Enable networking for package management:
```
dhclient -v
```

## 6. Package Management Recovery
Fix broken dependencies:
```
apt --fix-broken install   # For Debian-based systems
dnf distro-sync            # For Fedora-based systems
```

## 7. Kernel Issues
Boot into an older kernel version from GRUB menu. If successful, investigate the issue with the newer kernel.

## 8. Reset Root Password
If you've forgotten the root password:
```
passwd root
```

## 9. Recover GRUB
If GRUB is corrupted:
- a. Boot from a live USB
- b. Mount your root partition
- c. Chroot into it
- d. Reinstall GRUB:
```
grub-install /dev/sdX
update-grub
```

## 10. Repair Corrupted Files
Use tools like `dd` or `ddrescue` to recover data from failing drives.

## 11. Log Analysis
Check system logs for clues:
```
journalctl -xb          # For systemd-based systems
less /var/log/syslog    # For traditional syslog systems
```

## 12. Backup and Restore
Always maintain backups. Use tools like `rsync` or `tar` for backing up, and restore when needed.

## 13. Rescue Disk
Keep a rescue disk (like SystemRescue) handy for severe cases.

## 14. Data Recovery
For deleted files, use tools like `testdisk` or `photorec`.

## 15. Safe Mode and Single-User Mode
Boot into these modes for minimal system access to perform repairs.

## 16. Reinstallation
As a last resort, reinstall the system while preserving /home if possible.

Remember: Always approach system recovery cautiously. If you're unsure, consult documentation or seek help from the Linux community.
