# Performance Monitoring Tools (top, htop, vmstat)

## 1. top

Top is a dynamic real-time system monitoring tool that comes pre-installed on most Linux distributions. It provides a comprehensive overview of system resource usage.

Key features:
- Real-time view of system processes
- CPU and memory usage
- Load average
- Tasks statistics (running, sleeping, stopped, zombie)
- Uptime

Usage:
To start top, simply type `top` in the terminal.

Important commands within top:
- 'q': Quit
- 'h': Help
- 'k': Kill a process
- 'r': Renice a process
- 'f': Fields management
- 'o': Change sort order

Customization:
You can customize top's display by pressing 'f' to select which fields to show, and 'o' to change the sort order.

## 2. htop

Htop is an enhanced version of top with a more user-friendly interface and additional features. It's not usually pre-installed, so you may need to install it using your distribution's package manager.

Key features:
- Colorful and intuitive interface
- Mouse support
- Vertical and horizontal scrolling
- Tree view of processes
- Detailed CPU, memory, and swap usage

Usage:
To start htop, type `htop` in the terminal.

Important commands within htop:
- F1-F10: Various functions (help, setup, search, etc.)
- Space: Tag a process
- U: Show only processes of a specific user
- t: Tree view
- ]: Sort by CPU usage
- [: Sort by memory usage

Customization:
Htop offers extensive customization options. Press F2 to access the setup menu, where you can configure meters, colors, and display options.

## 3. vmstat

Vmstat (Virtual Memory Statistics) is a command-line tool that provides information about system processes, memory, paging, block I/O, traps, and CPU activity.

Key features:
- Compact output format
- Historical data
- Detailed memory statistics
- Disk I/O statistics
- CPU usage breakdown

Usage:
Basic syntax: vmstat [options] [delay [count]]

Example:
vmstat 5 3
This will display statistics every 5 seconds for 3 iterations.

Important columns in vmstat output:
- r: Number of runnable processes
- b: Number of processes in uninterruptible sleep
- swpd: Used swap space
- free: Free memory
- buff: Memory used as buffers
- cache: Memory used as cache
- si: Memory swapped in from disk
- so: Memory swapped out to disk
- bi: Blocks received from a block device
- bo: Blocks sent to a block device
- in: Interrupts per second
- cs: Context switches per second
- us, sy, id, wa: CPU time spent in user mode, kernel mode, idle, and waiting for I/O

Advanced usage:
- vmstat -s: Displays a table of various event counters and memory statistics
- vmstat -d: Shows disk statistics
- vmstat -p /dev/sda1: Displays statistics for a specific partition

## 4. Comparison and Use Cases:

### 1. top:
- Best for quick system overview
- Good for identifying resource-heavy processes
- Suitable for systems with limited resources

### 2. htop:
- Ideal for interactive use and detailed process management
- Better for systems with many processes
- More user-friendly for less experienced users

### 3. vmstat:
- Excellent for analyzing system performance over time
- Useful for identifying I/O or memory bottlenecks
- Good for scripting and automated monitoring

# 5. Best Practices:

- Regular monitoring: Use these tools regularly to establish a baseline for your system's performance.

- Combine tools: Each tool provides unique insights, so use them in combination for a comprehensive understanding.-3. Look for patterns: Pay attention to trends and patterns in resource usage over time.

- Customize: Tailor the tools to your specific needs by customizing their output and display options.

- Correlate with application logs: When you notice performance issues, correlate the data from these tools with your application logs for a fuller picture.

By mastering these Linux performance monitoring tools, you'll be well-equipped to diagnose and resolve system performance issues effectively.
