# Linux firewalls, focusing on UFW (Uncomplicated Firewall) and firewalld(systemd):

## 1. Introduction to Linux Firewalls
Linux firewalls are essential security tools that control incoming and outgoing network traffic based on predetermined security rules. They act as a barrier between trusted internal networks and untrusted external networks, such as the Internet.

## 2. Iptables: The Foundation
At the core of most Linux firewall solutions is iptables, a command-line utility for configuring the Linux kernel firewall. It works by defining chains of rules that filter packets based on various criteria.

Key concepts:
- Tables: filter, nat, mangle, raw
- Chains: INPUT, OUTPUT, FORWARD
- Rules: match criteria and target actions

While powerful, iptables can be complex for beginners, which led to the development of more user-friendly front-ends like UFW and firewalld.

## 3. UFW (Uncomplicated Firewall)

UFW is a simplified interface for managing iptables. It's designed to be easy to use while still providing robust firewall capabilities.

Key features:
- Simple command-line syntax
- Application profiles
- IPv6 support

Basic UFW commands:
- `sudo ufw enable`  # Enable the firewall
- `sudo ufw disable`  # Disable the firewall
- `sudo ufw status`  # Check firewall status
  `sudo ufw status numbered` # List the current ufw rules and their associated rule number
  `sudo ufw delete RULENUM` # Delete the firewall rule by number
- `sudo ufw allow 22`  # Allow incoming traffic on port 22 (SSH)
- `sudo ufw deny 80`  # Deny incoming traffic on port 80 (HTTP)
- `sudo ufw allow from 192.168.1.0/24`  # Allow traffic from a specific subnet
- `sudo ufw allow 32400/tcp` # Open port for Plex Server - ONLY accepting TCP traffic.


Advanced usage:
- Rate limiting: `sudo ufw limit 22/tcp`
- Logging: `sudo ufw logging on`
- Application profiles: `sudo ufw allow 'Apache Full'`

## 4. firewalld

firewalld is a dynamic firewall manager, primarily used in Red Hat-based distributions. It introduces the concept of zones, making it easier to manage complex network environments.

Key features:
- Zone-based configuration
- Runtime and permanent configuration options
- D-Bus interface for easy integration with other applications

- Basic firewalld commands:
- `sudo systemctl start firewalld`  # Start firewalld
- `sudo systemctl enable firewalld`  # Enable firewalld to start on boot
- `sudo firewall-cmd --state`  # Check firewalld status
- `sudo firewall-cmd --zone=public --add-service=http`  # Allow HTTP traffic in the public zone
- `sudo firewall-cmd --zone=internal --add-source=192.168.1.0/24`  # Add a source to the internal zone

Advanced usage:
- Custom services: `sudo firewall-cmd --new-service=myapp`
- Rich rules: `sudo firewall-cmd --add-rich-rule='rule family="ipv4" source address="192.168.1.0/24" port port="80" protocol="tcp" accept'`
- Direct interface (for complex iptables rules): `sudo firewall-cmd --direct --add-rule ipv4 filter INPUT 0 -p tcp --dport 22 -j ACCEPT`

## 5. Comparing UFW and firewalld

### UFW:
- Simpler, more straightforward for basic setups
- Ideal for single-host systems or simple network configurations
- Easier to learn for beginners
- Has a GUI (gufw) that can be installed. `sudo apt update && sudo apt install gufw`

### firewalld:
- More flexible and powerful for complex network setups
- Better suited for enterprise environments with multiple network zones
- Offers runtime and permanent configuration options

## 6. Best Practices
- Use the principle of least privilege: only open ports that are necessary
- Regularly review and update firewall rules
- Use logging to monitor firewall activity
- Combine firewall rules with other security measures (e.g., fail2ban for intrusion prevention)
- Keep your firewall software updated

## 7. Troubleshooting
- Check firewall logs: `/var/log/ufw.log` for UFW, `journalctl -u firewalld` for firewalld
- Use `iptables -L -v` to view current rules (works for both UFW and firewalld)
- Test connections with tools like `netcat` or `telnet`
- Temporarily disable the firewall to isolate issues

## 8. Advanced Topics (Coming Soon)
- Stateful vs. stateless firewalls
- Network Address Translation (NAT) configuration
- Setting up DMZ (Demilitarized Zone)
- Integrating with intrusion detection/prevention systems (IDS/IPS)
