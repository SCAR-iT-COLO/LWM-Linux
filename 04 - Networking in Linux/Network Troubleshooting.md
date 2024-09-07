# Linux Network Troubleshooting Guide

## 1. Basic Network Configuration Check:

   - Check IP address and network interface status:
      - `ip addr show` # This command displays all network interfaces, their IP addresses, and status.

   - Verify default gateway:
      - `ip route show` # Ensures your system knows how to route traffic outside the local network.

   - Check DNS configuration:
      - `cat /etc/resolv.conf` # Displays the DNS servers your system is using.

## 2. Connectivity Tests:

   - Ping test:
      - `ping -c 4 8.8.8.8` # Tests basic connectivity to Google's DNS server (or any other IP). Only pings 4 times (-c 4)

   - Traceroute:
      - `traceroute google.com` # Shows the path packets take to reach a destination.

   - DNS resolution test:
      - `nslookup google.com` # These test DNS resolution capabilities.
      - `dig google.com` # These test DNS resolution capabilities.
      
## 3. Advanced Diagnostic Tools:

   - netstat or ss:
      - `netstat -tulpn` # Display active network connections and listening ports.
      - `ss -tulpn` # Display active network connections and listening ports.

   - tcpdump:
      - `sudo tcpdump -i eth0` # eth0 is the Device name. Captures and displays packet data on a specified interface.

   - nmap:
      - `nmap -p- localhost` # Scans every port on the local machine (or any specified target).

## 4. Firewall Configuration:

   - Check iptables rules:
      - `sudo iptables -L -v -n` # Displays current firewall rules.

   - Temporarily disable firewall (for testing):
      - `sudo systemctl stop firewalld`  # Stops firewalld on the current boot - will start at next boot if enabled
      - `sudo ufw disable`  # Disables firewalld at system boot and stops it immedietely

## 5. Network Service Diagnostics:

   - Check service status:
      - `systemctl status networking`
      - `systemctl status NetworkManager`

   - Restart network service:
      - `sudo systemctl restart networking`
      - `sudo systemctl restart NetworkManager`

## 6. Network Interface Configuration:

   - Edit network interface configuration:
      - `sudo nano /etc/network/interfaces`  # for Debian-based systems
      - `sudo nano /etc/sysconfig/network-scripts/ifcfg-eth0`  # for Red Hat-based systems

   - Restart specific network interface:
      - `sudo ifdown eth0 && sudo ifup eth0`
      - `sudo ip link set eth0 down && sudo ip link set eth0 up`

## 7. Wireless Network Troubleshooting:

   - List available wireless networks:
      - `sudo iwlist wlan0 scan`

   - Check wireless interface details:
      - `iwconfig`

   - Monitor wireless connection in real-time:
      - `watch -n 1 iwconfig`

## 8. Advanced Network Analysis:

   - Wireshark: GUI-based packet analyzer
      Install with: 
      - `sudo apt-get install wireshark`  # on Debian-based systems
      - `sudo yum install wireshark`  # on Red Hat-based systems
      
   - iftop: Displays bandwidth usage on an interface
      - `sudo iftop -i eth0`

   - nethogs: Groups bandwidth by process
      - `sudo nethogs eth0`

## 9. Performance Testing:

   - iperf: Network performance measurement tool
      - `iperf -s`  # on server
      - `iperf -c server_ip`  # on client
      

   - speedtest-cli: Command-line interface for testing internet speed
      `speedtest-cli`

## 10. Log Analysis:
- `sudo tail -f /var/log/syslog`  # on Debian-based systems
- `sudo tail -f /var/log/messages`  # on Red Hat-based systems
- `sudo journalctl -b0`
- `sudo dmesg -k`
       
    - Network-specific logs:
       - `sudo tail -f /var/log/daemon.log`

## 11. Network Configuration Backup and Restore:

- Backup network configuration:
- `sudo tar -czvf network_config_backup.tar.gz /etc/network` # Create a file called network_config_backup.tar.gz from the /etc/network directory

- Restore network configuration:
- `sudo tar -xzvf network_config_backup.tar.gz -C /`

## 12. Troubleshooting Specific Issues:

- High latency: Use ping and traceroute to identify where delays occur.
- Packet loss: Use mtr (My TraceRoute) for a combination of ping and traceroute.
- DNS issues: Check /etc/hosts file and DNS server configurations.
- IP conflicts: Use arping to detect duplicate IP addresses on the network.

