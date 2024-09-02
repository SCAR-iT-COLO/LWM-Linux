# Linux Shutdown and reboot/restart procedure

## 1. Command Line Methods:

### a) Shutdown:
- To shut down immediately: `sudo shutdown -h now`
- To shut down after a delay: `sudo shutdown -h +m` (replace m with minutes)
- To shut down at a specific time: `sudo shutdown -h HH:MM` (24-hour format)

### b) Restart:
- To restart immediately: `sudo shutdown -r now` or `sudo reboot`
- To restart after a delay: `sudo shutdown -r +m` (replace m with minutes)
- To restart at a specific time: `sudo shutdown -r HH:MM` (24-hour format)

### c) Cancel a scheduled shutdown or restart:
- `sudo shutdown -c`

## 2. Using systemctl (for systemd-based distributions):

- Shutdown: `sudo systemctl poweroff`
- Restart: `sudo systemctl reboot`

## 3. Legacy commands (still work on most systems):

- Shutdown: `sudo halt` or `sudo poweroff`
- Restart: `sudo reboot`

## 4. GUI Methods:

Most desktop environments (GNOME, KDE, Xfce, etc.) have a menu option for shutting down or restarting. Usually found in the main menu or by clicking on the user name/icon.

## 5. Emergency Immediate Shutdown:

In case of an unresponsive system, you can use the magic SysRq key combinations:
- Hold Alt + SysRq (usually Print Screen), then press these keys in sequence: R E I S U B
- This safely syncs data, unmounts filesystems, and reboots the system

## 6. Sending Signals:

You can use the `kill` command to send signals to the init process:
- Shutdown: `sudo kill -s SIGINT 1`
- Restart: `sudo kill -s SIGTERM 1`

## 7. Additional Options and Considerations:

a) Force shutdown (use cautiously): `sudo shutdown -h -f now`
b) Schedule a shutdown message: `sudo shutdown -h +m "System will shutdown in m minutes"`
c) Shut down without sudo (if configured): `shutdown -h now`

## 8. Shutting down remote systems:

- SSH into the system and use any of the above commands
- Use `ssh user@host "sudo shutdown -h now"` from another machine

## 9. Checking shutdown/restart history:

- View last shutdown: `last -x shutdown`
- View last reboot: `last reboot`
- Check system logs: `journalctl --since "1 hour ago" | grep -i "shut down\|reboot"`

## 10. Best Practices:

- Always ensure all important data is saved before shutting down or restarting
- Close all running applications to prevent data loss
- For servers, notify users before scheduling a shutdown or restart
- Use delayed shutdowns to give time for important processes to complete
- Regularly check system logs for any shutdown/restart issues

- [(1) How to Reboot or Shut Down Linux Using the Command Line.)](https://www.howtogeek.com/411925/how-to-reboot-or-shut-down-linux-using-the-command-line/.)
- [(2) How to reboot, shutdown, log off PC from Terminal by command line in](https://www.fosslinux.com/1115/how-to-reboot-shutdown-log-off-pc-from-terminal-by-command-line-in-ubuntu-and-linux-mint.htm.)
- [(3) How do I shut down or reboot from a terminal? - Ask Ubuntu.](https://askubuntu.com/questions/187071/how-do-i-shut-down-or-reboot-from-a-terminal.)
- [(4) 5 Linux Commands to Shutdown and Reboot the System.](https://www.binarytides.com/linux-command-shutdown-reboot-restart-system/.)
