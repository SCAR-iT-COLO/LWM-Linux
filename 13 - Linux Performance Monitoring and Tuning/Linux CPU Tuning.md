# Linux CPU tuning

## 1. Understanding CPU Governors

CPU governors control the CPU frequency scaling on Linux systems. The main governors are:

- performance: Runs the CPU at maximum frequency
- powersave: Runs the CPU at minimum frequency
- ondemand: Dynamically scales CPU frequency based on system load
- conservative: Similar to ondemand, but scales frequency more gradually
- schedutil: Uses the CPU scheduler for frequency scaling decisions

To view available governors:
```bash
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_governors
```

To set a governor:
```bash
sudo cpupower frequency-set -g <governor>
```

## 2. CPU Frequency Scaling

You can manually set CPU frequencies:

View available frequencies:
```bash
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_available_frequencies
```

Set minimum and maximum frequencies:
```bash
sudo cpupower frequency-set --min <freq> --max <freq>
```

## 3. CPU Affinity

CPU affinity allows you to bind processes to specific CPU cores:

```bash
taskset -c 0,1 <command>  # Run command on cores 0 and 1
```

## 4. Nice and Ionice

Adjust process priorities:

```bash
nice -n <value> <command>  # Set CPU scheduling priority (-20 to 19)
ionice -c <class> -n <value> <command>  # Set I/O scheduling priority
```

## 5. CPU Isolation

Isolate CPUs from the scheduler to dedicate them to specific tasks:

Add to kernel boot parameters:
```bash
isolcpus=2,3
```

## 6. IRQ Balancing

Manage interrupt request (IRQ) distribution:

Disable IRQ balancing:
```bash
sudo service irqbalance stop
```

Manually set IRQ affinity:
```bash
echo <cpu_mask> > /proc/irq/<irq_number>/smp_affinity
```

## 7. CPU Power Management

Control CPU power-saving features:

Disable C-states:
```bash
echo 1 > /sys/devices/system/cpu/cpu0/cpuidle/state1/disable
```

Adjust Intel P-states:
```bash
echo passive > /sys/devices/system/cpu/intel_pstate/status
```

## 8. Kernel Parameters

Adjust various kernel parameters for CPU performance:

Edit /etc/sysctl.conf:
```ini
kernel.sched_migration_cost_ns = 5000000
kernel.sched_autogroup_enabled = 0
kernel.sched_wakeup_granularity_ns = 15000000
```

Apply changes:
```bash
sudo sysctl -p
```

## 9. CPU Topology

Understand your CPU topology:
```bash
lscpu
lstopo
```

## 10. Monitoring and Profiling

Use tools to monitor CPU performance:

- top/htop: Real-time system monitor
- perf: Linux profiling tool
- stress-ng: CPU stress testing tool
- s-tui: Terminal-based CPU monitoring

## 11. NUMA (Non-Uniform Memory Access)

For multi-socket systems, manage NUMA settings:

View NUMA info:
```bash
numactl --hardware
```

Run a command with NUMA policy:
```bash
numactl --cpunodebind=0 --membind=0 <command>
```

## 12. Compiler Optimizations

When compiling software, use CPU-specific optimizations:

GCC flags:
```bash
-march=native -mtune=native
```

## 13. CPU Vulnerabilities Mitigations

Control CPU vulnerability mitigations:

View current mitigations:
```bash
grep . /sys/devices/system/cpu/vulnerabilities/*
```

Disable mitigations (may impact security):
Add to kernel boot parameters:
```bash
mitigations=off
```

This guide covers the main aspects of CPU tuning on Linux. Remember that optimal settings depend on your specific hardware and workload. Always test thoroughly and monitor system performance when making changes.
