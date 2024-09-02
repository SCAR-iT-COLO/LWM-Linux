# Linux Basic Network Configuration

## 1. Network Interfaces

Linux uses network interfaces to communicate with networks. Common interfaces include:

- eth0, eth1, etc.: Ethernet interfaces
- wlan0, wlan1, etc.: Wireless interfaces
- lo: Loopback interface

To list network interfaces:

```
ip link show
```

or

```
ifconfig -a
```

## 2. IP Address Configuration

### Temporary IP configuration:

- To set an IP address temporarily:

```
sudo ip addr add 192.168.1.100/24 dev eth0
```

- To remove an IP address:

```
sudo ip addr del 192.168.1.100/24 dev eth0
```

###  Permanent IP configuration:

Edit the network configuration file (location varies by distribution):

- Ubuntu/Debian: /etc/network/interfaces
- CentOS/RHEL: /etc/sysconfig/network-scripts/ifcfg-eth0

Example configuration:

```
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
```

## 3. DHCP Configuration

For dynamic IP assignment, use DHCP:

```
auto eth0
iface eth0 inet dhcp
```

## 4. Network Manager

Many modern Linux distributions use Network Manager for easier network configuration. You can use the command-line tool 'nmcli' or GUI tools to manage connections.

## 5. Hostname Configuration

Set the hostname:

```
sudo hostnamectl set-hostname new-hostname
```

Update /etc/hosts file to include the new hostname.

## 6. DNS Configuration

Edit /etc/resolv.conf to set DNS servers:

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

Note: This file may be overwritten by DHCP. For permanent changes, configure your network manager or DHCP client.

## 7. Routing

View routing table:

```
ip route show
```

Add a static route:

```
sudo ip route add 10.0.0.0/24 via 192.168.1.1 dev eth0
```

## 8. Firewall Configuration

Most Linux distributions use iptables or nftables. Ubuntu uses ufw (Uncomplicated Firewall) as a frontend.

Enable UFW:

```
sudo ufw enable
```

Allow incoming SSH:

```
sudo ufw allow ssh
```

## 9. Network Diagnostics

- ping: Test connectivity
- traceroute: Trace packet route
- netstat or ss: Display network connections
- tcpdump: Capture and analyze network traffic

## 10. Network Service Management

Start/stop network service:

```
sudo systemctl start networking
sudo systemctl stop networking
```

Enable/disable network service at boot:

```
sudo systemctl enable networking
sudo systemctl disable networking
```

## 11. Wireless Network Configuration

Use 'iwconfig' to configure wireless interfaces:

```
sudo iwconfig wlan0 essid "NetworkName" key s:password
```

For WPA networks, use 'wpa_supplicant'.

## 12. Network Bonding

Combine multiple network interfaces for redundancy or increased throughput. Edit /etc/network/interfaces:

```
auto bond0
iface bond0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    bond-slaves eth0 eth1
    bond-mode active-backup
    bond-miimon 100
    bond-primary eth0
```


- [(1) The Ultimate Guide to Linux Mint Network Configuration.](https://www.fosslinux.com/105545/the-ultimate-guide-to-linux-mint-network-configuration.htm.)
- [(2) How to set up an Internet Connection in Linux Mint?.](https://unix.stackexchange.com/questions/132747/how-to-set-up-an-internet-connection-in-linux-mint.)
- [(3) How to Share Files and Folders on a Linux Mint Network.](https://www.fosslinux.com/103443/how-to-easily-share-files-and-folders-on-a-linux-mint-network.htm.)
- [(4) Linux Mint - Community.](https://community.linuxmint.com/tutorial/view/1966.)
- [(5) Configure Network in Debian / Ubuntu / LinuxMint - ITzGeek.](https://www.itzgeek.com/how-tos/linux/ubuntu-how-tos/configure-network-in-ubuntu-14-04-linux-mint.html.)

