# Understanding and Using SystemD

### 1. Introduction to systemd

systemd is an init system and system manager that has become the standard for many Linux distributions. It was designed to overcome limitations in the traditional SysV init system, providing faster boot times, dependency-based service control, and a unified interface for managing system services.

### 2. Core Concepts

- Units: The basic building blocks of systemd. Units can represent services, devices, mount points, and more.
- Dependencies: systemd manages relationships between units, ensuring they start in the correct order.
- Targets: Groups of units that represent a specific system state (similar to runlevels in SysV init).
- Sockets: Allow for service activation on demand.
- Timers: Provide cron-like functionality for scheduling tasks.

### 3. Unit Files

Unit files are configuration files that define how systemd should manage a unit. They are typically located in /etc/systemd/system/ or /usr/lib/systemd/system/.

Structure of a basic service unit file:

```ini
[Unit]
Description=My Custom Service
After=network.target

[Service]
ExecStart=/path/to/your/script.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

### 4. Basic systemd Commands

- systemctl: The main command for interacting with systemd
- journalctl: Used for viewing logs
- systemd-analyze: Analyzes system boot-up performance

Common systemctl commands:
```
systemctl start service-name
systemctl stop service-name
systemctl restart service-name
systemctl status service-name
systemctl enable service-name
systemctl disable service-name
```

### 5. Managing Services

To create a new service:
1. Create a unit file in /etc/systemd/system/ (e.g., myservice.service)
2. Define the service using the structure shown earlier
3. Reload the systemd manager: `systemctl daemon-reload`
4. Start and enable the service: `systemctl start myservice && systemctl enable myservice`

### 6. System Boot and Target Units

systemd uses target units to manage the boot process. Key targets include:
- poweroff.target
- rescue.target
- multi-user.target
- graphical.target

To change the default target:
```
systemctl set-default graphical.target
```

### 7. Logging with journald

journald is systemd's logging system. Key features:
- Collects messages from the kernel, services, and applications
- Indexes logs for fast searching
- Supports structured logging

Basic journalctl usage:
```
journalctl -u service-name  # View logs for a specific service
journalctl -f  # Follow new log entries
journalctl --since "1 hour ago"  # View recent logs
```

### 8. Advanced Features

- Socket Activation: Services start on-demand when a client connects to their socket.
- Resource Control: Limit CPU, memory, and other resources for services.
- Security Features: Restrict service permissions and access.

Example of resource control in a unit file:
```ini
[Service]
ExecStart=/path/to/your/script.sh
CPUQuota=20%
MemoryLimit=100M
```

### 9. Troubleshooting

- Check service status: `systemctl status service-name`
- View recent logs: `journalctl -u service-name -n 50 --no-pager`
- List failed units: `systemctl --failed`
- Check boot time: `systemd-analyze`
