# Linux Filesystem Hierarchy Standard (LFHS)

The Linux Filesystem Hierarchy Standard (FHS) defines the directory structure and directory contents in Linux and other Unix-like operating systems. It is maintained by the Linux Foundation and provides consistency across distributions. Let's explore the main directories and their purposes:

## 1. / (Root Directory)
The root directory is the top-level directory of the filesystem. All other directories are subdirectories of the root.

## 2. /bin (Essential User Binaries)
Contains essential command binaries that need to be available in single-user mode. Examples include ls, cp, and pwd.

## 3. /boot (Boot Loader Files)
Contains files needed for the boot process, including the kernel, initrd, and boot loader configuration.

## 4. /dev (Device Files)
Contains device files, which are interfaces for device drivers. Examples include /dev/sda for the first SATA drive and /dev/tty for terminals.

## 5. /etc (Configuration Files)
Stores system-wide configuration files and scripts. Examples include /etc/passwd for user information and /etc/fstab for filesystem information.

## 6. /home (User Home Directories)
Contains home directories for regular users. Each user typically has a subdirectory here, like /home/username.

## 7. /lib (Essential Shared Libraries)
Holds library files needed by the binaries in /bin and /sbin.

## 8. /media (Removable Media)
Mount point for removable media such as USB drives and CD-ROMs.

## 9. /mnt (Temporary Mount Points)
Used for temporarily mounted filesystems.

## 10. /opt (Optional Software)
Reserved for the installation of add-on application software packages.

## 11. /proc (Process Information)
A virtual filesystem providing process and kernel information as files.

## 12. /root (Root User Home Directory)
Home directory for the root user.

## 13. /run (Run-time Variable Data)
Contains variable data files describing the system since the last boot.

## 14. /sbin (System Binaries)
Similar to /bin, but contains binaries essential for system administration, usually to be run by root.

## 15. /srv (Service Data)
Contains data for services provided by the system.

## 16. /sys (System Information)
A virtual filesystem providing a standardized interface to kernel objects.

## 17. /tmp (Temporary Files)
Directory for temporary files. Often cleared on reboot.

## 18. /usr (User Programs)
Contains the majority of user utilities and applications. It has several subdirectories:
   - /usr/bin: Non-essential command binaries
   - /usr/lib: Libraries for /usr/bin and /usr/sbin
   - /usr/local: Local hierarchy for system administrators
   - /usr/sbin: Non-essential system binaries
   - /usr/share: Architecture-independent data

## 19. /var (Variable Files)
Contains variable data files, including logs (/var/log), temporary email files (/var/mail), and spooled files (/var/spool).

## 20. Key Principles of FHS:
- 1. Separation of core system files from user files
- 2. Consistency across distributions
- 3. Backward compatibility
- 4. Flexibility for system administrators

## 21. Benefits of FHS:
- 1. Easier system administration
- 2. Improved security through proper file organization
- 3. Compatibility across different Linux distributions
- 4. Easier software development and deployment

[LFHS](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)
