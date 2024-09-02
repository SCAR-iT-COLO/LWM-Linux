# Linux Disk Monitoring and Tuning

## 1. Disk Monitoring Tools

### iostat
iostat provides detailed I/O statistics for devices and partitions. It shows CPU utilization and disk I/O statistics.

Usage:
```bash
iostat [options] [interval] [count]
```

Key metrics:
- %util: Percentage of CPU time during which I/O requests were issued
- r/s and w/s: Read and write requests per second
- rkB/s and wkB/s: Read and write kilobytes per second

### iotop
iotop is an interactive I/O monitoring tool that shows per-process I/O usage.

Usage:
```bash
iotop
```

### dstat
dstat is a versatile tool for generating system resource statistics.

Usage:
```bash
dstat --disk --io --disk-util
```

### vmstat
vmstat reports information about processes, memory, paging, block I/O, traps, and CPU activity.

Usage:
```bash
vmstat [interval] [count]
```

### fdisk
fdisk is a dialog-driven program for creation and manipulation of partition tables.

Usage:
```bash
fdisk -l
```

## 2. Disk Performance Testing

### dd
dd can be used for simple disk read/write performance tests.

Example (write test):
```bash
dd if=/dev/zero of=testfile bs=1G count=1 oflag=dsync
```

Example (read test):
```bash
dd if=testfile of=/dev/null bs=1G count=1
```

### fio
fio is a flexible I/O tester for benchmark and stress/hardware verification.

Example:
```bash
fio --name=random-write --ioengine=posixaio --rw=randwrite --bs=4k --size=4g --numjobs=1 --runtime=60 --time_based --end_fsync=1
```

## 3. File System Monitoring

### df
df reports file system disk space usage.

Usage:
```bash
df -h
```

### du
du estimates file and directory space usage.

Usage:
```bash
du -sh /path/to/directory
```

## 4. Disk Tuning Techniques

### I/O Scheduler
Linux offers different I/O schedulers. Common ones include:
- CFQ (Completely Fair Queuing)
- Deadline
- NOOP

To check the current scheduler:
```bash
cat /sys/block/sda/queue/scheduler
```

To change the scheduler:
```bash
echo "deadline" > /sys/block/sda/queue/scheduler
```

### Read-ahead
Adjust the read-ahead value to optimize for your workload:

```bash
blockdev --getra /dev/sda
blockdev --setra 8192 /dev/sda
```

### Swappiness
Reduce swappiness to minimize disk writes:

```
sysctl vm.swappiness=10
```

### Disk Cache
Adjust the ratio of cached dirty memory:

```bash
sysctl -w vm.dirty_ratio=10
sysctl -w vm.dirty_background_ratio=5
```

### TRIM (for SSDs)
Enable TRIM for SSDs to maintain performance:

```bash
fstrim -v /
```

Or add the `discard` option to the mount options in /etc/fstab.

### Journaling
For ext4 file systems, you can disable journaling for better write performance (at the cost of data integrity):

```bash
tune2fs -O ^has_journal /dev/sda1
```

### Noatime
Use the `noatime` mount option to reduce disk writes:

In /etc/fstab:
```ini
UUID=xxx / ext4 defaults,noatime 0 1
```

## 5. Monitoring Tools for Long-term Analysis

### sysstat
sysstat includes tools like sar (System Activity Reporter) for long-term performance monitoring.

To enable data collection:
```bash
systemctl enable sysstat
systemctl start sysstat
```

To view collected data:
```bash
sar -d
```

### Prometheus + Node Exporter + Grafana
For a more comprehensive monitoring solution:
- Install and configure Prometheus
- Set up Node Exporter on monitored systems
- Create dashboards in Grafana for visualization

## 6. Best Practices

### Regular Maintenance
- Run fsck regularly on unmounted file systems
- Use SMART monitoring tools for early warning of disk failures
- Perform regular backups

### Capacity Planning
- Monitor disk usage trends
- Plan for capacity increases before running out of space

### RAID Considerations
- Use appropriate RAID levels for your use case
- Monitor RAID health and replace failed disks promptly

### SSD-specific Considerations
- Enable TRIM
- Monitor SSD wear levels
- Consider over-provisioning for write-heavy workloads

This guide covers the basics of Linux disk monitoring and tuning. Remember that optimal settings depend on your specific hardware and workload. Always test changes in a non-production environment first.
