
# RAID and LVM 

## 1. RAID (Redundant Array of Independent Disks)

RAID is a technology that combines multiple disk drive components into a logical unit for data redundancy and performance improvement. 

Types of RAID:

### a) RAID 0 (Striping):
- Data is split across multiple disks
- Improves performance but no redundancy
- Minimum 2 disks required

### b) RAID 1 (Mirroring):
- Data is duplicated on two or more disks
- Provides redundancy but no performance improvement for writes
- Minimum 2 disks required

### c) RAID 5 (Striping with parity):
- Data and parity information are striped across all disks
- Good balance of performance and redundancy
- Can survive one disk failure
- Minimum 3 disks required

### d) RAID 6 (Striping with double parity):
- Similar to RAID 5 but with two parity blocks
- Can survive two disk failures
- Minimum 4 disks required

### e) RAID 10 (Stripe of mirrors):
- Combines RAID 1 and RAID 0
- Provides both redundancy and performance improvement
- Minimum 4 disks required

## Setting up RAID in Linux:

### 1. Install mdadm:
```
sudo apt-get install mdadm
```

### 2. Create a RAID array (example for RAID 5):
```
sudo mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd
```

### 3. Create a filesystem on the RAID array:
```
sudo mkfs.ext4 /dev/md0
```

### 4. Mount the RAID array:
```
sudo mount /dev/md0 /mnt/raid
```

### 5. Save the RAID configuration:
```
sudo mdadm --detail --scan >> /etc/mdadm/mdadm.conf
```

## 2. LVM (Logical Volume Management)

LVM is a device mapper framework that provides logical volume management for the Linux kernel. It allows for more flexible disk space management.

Key concepts:

- a) Physical Volume (PV): Physical disks or partitions
- b) Volume Group (VG): Group of physical volumes
- c) Logical Volume (LV): Virtual partitions created from a volume group

Setting up LVM:

### 1. Install LVM:
```
sudo apt-get install lvm2
```

### 2. Create Physical Volumes:
```
sudo pvcreate /dev/sdb /dev/sdc
```

### 3. Create a Volume Group:
```
sudo vgcreate myvg /dev/sdb /dev/sdc
```

### 4. Create Logical Volumes:
```
sudo lvcreate -n mylv1 -L 50G myvg
sudo lvcreate -n mylv2 -l 100%FREE myvg
```

### 5. Create filesystems on Logical Volumes:
```
sudo mkfs.ext4 /dev/myvg/mylv1
sudo mkfs.ext4 /dev/myvg/mylv2
```

### 6. Mount Logical Volumes:
```
sudo mount /dev/myvg/mylv1 /mnt/lv1
sudo mount /dev/myvg/mylv2 /mnt/lv2
```

Advantages of LVM:

- 1. Flexible capacity management
- 2. Easy resizing of logical volumes
- 3. Snapshots for backup purposes
- 4. Striping and mirroring capabilities

Combining RAID and LVM:

You can use RAID as the underlying storage for LVM, providing both redundancy and flexibility:

- 1. Create a RAID array
- 2. Use the RAID array as a Physical Volume for LVM
- 3. Create Volume Groups and Logical Volumes on top of the RAID array

Example:

```
sudo mdadm --create --verbose /dev/md0 --level=5 --raid-devices=3 /dev/sdb /dev/sdc /dev/sdd
sudo pvcreate /dev/md0
sudo vgcreate myvg /dev/md0
sudo lvcreate -n mylv1 -L 100G myvg
sudo mkfs.ext4 /dev/myvg/mylv1
sudo mount /dev/myvg/mylv1 /mnt/data
```

This setup provides the redundancy of RAID 5 with the flexibility of LVM.

### Maintenance and Monitoring:

#### 1. RAID:
- Check RAID status: `cat /proc/mdstat`
- Detailed RAID info: `sudo mdadm --detail /dev/md0`

#### 2. LVM:
- Display PV info: `sudo pvdisplay`
- Display VG info: `sudo vgdisplay`
- Display LV info: `sudo lvdisplay`
