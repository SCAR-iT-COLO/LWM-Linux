# Network Troubleshooting (Nmap)

Nmap (Network Mapper) is a powerful open-source tool for network discovery and security auditing. It's essential for network administrators and security professionals. This guide will cover various aspects of using Nmap for network troubleshooting.

## 1. Basic Nmap Usage

Syntax: nmap [scan type] [options] {target}

Example: nmap 192.168.1.1

This performs a basic scan on the specified IP address.

## 2. Common Scan Types

- a) TCP SYN Scan (-sS): Default scan type, relatively stealthy.
   nmap -sS 192.168.1.1

- b) TCP Connect Scan (-sT): Full TCP handshake, less stealthy but more reliable.
   nmap -sT 192.168.1.1

- c) UDP Scan (-sU): Scan UDP ports.
   nmap -sU 192.168.1.1

- d) Ping Scan (-sn): Determine which hosts are online without port scanning.
   nmap -sn 192.168.1.0/24

## 3. Port Specification

- a) Scan specific ports:
   nmap -p 80,443,8080 192.168.1.1

- b) Scan top N ports:
   nmap --top-ports 100 192.168.1.1

- c) Scan all 65535 ports:
   nmap -p- 192.168.1.1

## 4. OS and Version Detection

- a) OS Detection:
   nmap -O 192.168.1.1

- b) Version Detection:
   nmap -sV 192.168.1.1

- c) Combine OS and Version Detection:
   nmap -A 192.168.1.1

## 5. Output Options

- a) Save output to a file:
   nmap -oN output.txt 192.168.1.1

- b) Save in XML format:
   nmap -oX output.xml 192.168.1.1

- c) Save in all major formats:
   nmap -oA output 192.168.1.1

## 6. Timing and Performance

Nmap has predefined timing templates from T0 (slowest) to T5 (fastest):
nmap -T4 192.168.1.1

## 7. Firewall/IDS Evasion Techniques

- a) Fragment packets:
   nmap -f 192.168.1.1

- b) Use a decoy:
   nmap -D RND:10 192.168.1.1

- c) Spoof MAC address:
   nmap --spoof-mac 00:11:22:33:44:55 192.168.1.1

## 8. Script Engine

Nmap has a powerful scripting engine for advanced tasks:

- a) Use default scripts:
   nmap -sC 192.168.1.1

- b) Run specific scripts:
   nmap --script=http-title 192.168.1.1

- c) Update script database:
   nmap --script-updatedb

## 9. Troubleshooting Specific Issues

- a) Checking for open ports:
   nmap -p- 192.168.1.1

- b) Identifying services running on non-standard ports:
   nmap -sV -p- 192.168.1.1

- c) Detecting potential vulnerabilities:
   nmap --script vuln 192.168.1.1

- d) Checking for misconfigured firewalls:
   nmap -sA 192.168.1.1

- e) Identifying live hosts on a network:
   nmap -sn 192.168.1.0/24

## 10. Best Practices

- Always obtain permission before scanning networks you don't own.
- Use less intrusive scans first, then progress to more comprehensive scans.
- Regularly update Nmap to get the latest features and security updates.
- Combine Nmap with other tools for a comprehensive network analysis.
- Document your findings and create baseline scans for future comparison.

## 11. Advanced Techniques

- a) Scan using IPv6:
   nmap -6 2001:db8::1

- b) Perform a traceroute:
   nmap --traceroute 192.168.1.1

- c) Scan through a proxy:
   nmap --proxy socks4://proxy-server:1080 192.168.1.1

- d) Aggressive scan (combines OS detection, version scanning, script scanning, and traceroute):
   nmap -A 192.168.1.1

By mastering these Nmap techniques, you can effectively troubleshoot various network issues, from connectivity problems to security vulnerabilities. Remember to use Nmap responsibly and ethically, always respecting network owners' privacy and security.
