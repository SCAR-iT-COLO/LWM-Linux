# Disk Management and Partitions in Linux

1. Introduction to Disk Management in Linux
2. Understanding Partitions
3. Partition Table Types
4. Linux Filesystem Hierarchy
5. Common Disk Management Tools
6. Basic Disk Operations
7. Advanced Disk Operations
8. Best Practices and Considerations

## 1. Introduction to Disk Management in Linux

Disk management in Linux involves organizing and maintaining storage devices connected to your system. This includes tasks such as creating, resizing, and deleting partitions, formatting filesystems, and mounting storage devices.

## 2. Understanding Partitions

A partition is a logical division of a physical storage device. Partitions allow you to:
- Separate the operating system from user data
- Install multiple operating systems on a single drive
- Organize data more efficiently
- Improve system performance and security

Common partition types in Linux include:
- Root (/)
- Swap
- /home
- /boot
- /var

## 3. Partition Table Types

There are two main types of partition tables:

### a. MBR (Master Boot Record):
- Limited to 4 primary partitions
- Maximum partition size of 2TB
- Used in legacy BIOS systems

### b. GPT (GUID Partition Table):
- Supports up to 128 partitions
- Allows for much larger partition sizes
- Used in modern UEFI systems

## 4. Linux Filesystem Hierarchy

Linux follows a standardized directory structure:
- /: Root directory
- /home: User home directories
- /etc: System configuration files
- /var: Variable data (logs, temporary files)
- /boot: Boot loader files
- /mnt and /run/media: Mount points for removable devices

## 5. Common Disk Management Tools

Linux provides several tools for disk management:

### a. Command-line tools:
- fdisk: Partition table manipulator
- parted: Versatile partition tool
- lsblk: List block devices
- df: Report "disk free" in bytes. add "-h" option for human readable
- du: Estimate file space usage for current directory.  Add "-h" option for human readable file sizes.

### b. Graphical tools:
- GParted: GNOME Partition Editor
- KDE Partition Manager

## 6. Basic Disk Operations

### a. Viewing disk information:
```
lsblk
```
```
fdisk -l
```

### b. Creating a new partition:
```
sudo fdisk /dev/sdX
```
(Replace X with the appropriate letter).  Follow prompts inside fdisk to create new blank partition.

### c. Formatting a partition:
```
sudo mkfs.ext4 /dev/sdXY
```
(Replace X and Y with appropriate letters/numbers)

### d. Mounting a partition:
```
sudo mount /dev/sdXY /mnt/mountpoint
```

### e. Unmounting a partition:
```
sudo umount /mnt/mountpoint
```

## 7. Advanced Disk Operations

### a. Resizing partitions:
Use GParted or command-line tools like resize2fs for ext filesystems.

### b. LVM (Logical Volume Management):
LVM allows for more flexible disk management, including:
- Spanning volumes across multiple disks
- Easy resizing of logical volumes
- Creating snapshots

### c. RAID (Redundant Array of Independent Disks):
Linux supports software RAID for improved performance and data redundancy in hardware and software formats.

### d. Encrypting partitions:
Use LUKS (Linux Unified Key Setup) for full-disk encryption.

## 8. Best Practices and Considerations

a. Regular backups: Always back up important data before making changes to disk partitions.

b. Plan your partitioning scheme: Consider your needs for separate /home, /var, or /opt partitions.

c. Use appropriate filesystem types: Choose between ext4, XFS, Btrfs, or others based on your requirements.

d. Monitor disk health: Use tools like smartctl to check for potential drive failures.

e. Keep your system updated: Regular updates can improve disk management tools and fix bugs.

f. Be cautious with root privileges: Disk management often requires root access, so be careful to avoid accidental data loss.
