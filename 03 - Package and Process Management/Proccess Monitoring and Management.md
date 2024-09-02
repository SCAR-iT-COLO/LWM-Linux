# Process Monitoring and Management in Linux

### 1. Viewing Running Processes

Let's start with the basic commands to view running processes:

- ps - Process Status
The 'ps' command provides a snapshot of current processes.

Basic usage:
```
ps
```

Common options:
- `ps aux`: Shows all processes for all users
- `ps -ef`: Similar to aux, but in a different format
- `ps lax`: Provides more detailed information

- top - Table of Processes
'top' provides a real-time, dynamic view of running processes.

Basic usage:
```
top
```

In top, you can use:
- 'q' to quit
- 'k' to kill a process (you'll be prompted for the PID)
- 'r' to renice (change priority) of a process

- htop - Interactive Process Viewer
'htop' is an improved version of 'top' with a more user-friendly interface.

Install it (if not already installed):
```
sudo apt install htop  # For Debian/Ubuntu
sudo yum install htop  # For CentOS/RHEL
```

Run it:
```
htop
```

### 2. Process Management

- kill - Terminate a Process
The 'kill' command sends a signal to a process, by default the TERM signal.

Basic usage:
```
kill PID
```

Common signals:
- SIGTERM (15): Graceful termination
- SIGKILL (9): Forceful termination

Example:
```
kill -9 1234
```

- killall - Kill Processes by Name
'killall' allows you to kill all processes with a given name.

Example:
```
killall firefox
```

- pkill - Kill Processes Based on Name and Other Attributes
'pkill' is more flexible than killall, allowing you to kill processes based on various attributes.

Example:
```
pkill -u username firefox
```

- nice and renice - Adjust Process Priority
'nice' starts a process with a specified priority, while 'renice' changes the priority of a running process.

Nice values range from -20 (highest priority) to 19 (lowest priority).

Example:
```
nice -n 10 command  # Start 'command' with lower priority
renice -n 5 -p PID  # Change priority of running process
```

### 3. Background and Foreground Processes

- Start a process in the background:
```
command &
```

- Move a running process to the background:
Press Ctrl+Z

- Bring a background process to the foreground:
```
fg %job_number
```

- List background jobs:
```
jobs
```

### 4. Advanced Monitoring Tools

- iotop - I/O Monitoring
'iotop' shows I/O usage by processes.

Install:
```
sudo apt install iotop  # For Debian/Ubuntu
sudo yum install iotop  # For CentOS/RHEL
```

Run:
```
sudo iotop
```

- nethogs - Network Monitoring
'nethogs' shows network usage by process.

Install:
```
sudo apt install nethogs  # For Debian/Ubuntu
sudo yum install nethogs  # For CentOS/RHEL
```

Run:
```
sudo nethogs
```

- lsof - List Open Files
'lsof' lists open files and the processes using them.

Example (list all network connections):
```
sudo lsof -i
```

### 5. System Monitoring

- free - Display Amount of Free and Used Memory
```
free -h  # -h for human-readable format
```

- vmstat - Report Virtual Memory Statistics
```
vmstat 1  # Report every second
```

- iostat - Report CPU Statistics and I/O Statistics
```
iostat 1  # Report every second
```

### 6. Process Tracking and Analysis

- strace - Trace System Calls and Signals
'strace' is useful for diagnosing problems with processes.

Example:
```
strace command
```

- ltrace - Library Call Tracer
'ltrace' is similar to strace but for library calls.

Example:
```
ltrace command
```

### 7. Continuous Monitoring with watch

The 'watch' command allows you to run any command periodically, showing output in fullscreen.

Example (update process list every 2 seconds):
```
watch -n 2 'ps aux | sort -nrk 3,3 | head -n 5'
```
