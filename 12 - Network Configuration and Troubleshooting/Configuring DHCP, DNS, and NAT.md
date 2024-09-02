# Configuring DHCP, DNS, and NAT

## 1. DHCP (Dynamic Host Configuration Protocol)

DHCP is used to automatically assign IP addresses and network configuration to devices on a network. In Linux, we typically use the ISC DHCP server.

### Installation:
```
sudo apt-get install isc-dhcp-server
```

### Configuration:
Edit the main configuration file `/etc/dhcp/dhcpd.conf`:

```
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option routers 192.168.1.1;
  option domain-name-servers 8.8.8.8, 8.8.4.4;
  default-lease-time 600;
  max-lease-time 7200;
}
```

This configuration:
- Defines a subnet
- Sets the IP range for DHCP clients
- Specifies the router (gateway)
- Sets DNS servers
- Configures lease times

### Start the DHCP server:
```
sudo systemctl start isc-dhcp-server
```

### Enable it to start on boot:
```
sudo systemctl enable isc-dhcp-server
```

## 2. DNS (Domain Name System)

For DNS, we'll use BIND (Berkeley Internet Name Domain).

### Installation:
```
sudo apt-get install bind9
```

### Configuration:
Edit the main configuration file `/etc/bind/named.conf.options`:

```
options {
    directory "/var/cache/bind";
    forwarders {
        8.8.8.8;
        8.8.4.4;
    };
    dnssec-validation auto;
    auth-nxdomain no;
    listen-on-v6 { any; };
};
```

This configuration sets up BIND to forward DNS queries to Google's DNS servers.

For a local zone, edit `/etc/bind/named.conf.local`:

```
zone "example.com" {
    type master;
    file "/etc/bind/db.example.com";
};
```

### Then create the zone file `/etc/bind/db.example.com`:

```
$TTL    604800
@       IN      SOA     ns1.example.com. admin.example.com. (
                  3     ; Serial
             604800     ; Refresh
              86400     ; Retry
            2419200     ; Expire
             604800 )   ; Negative Cache TTL
;
@       IN      NS      ns1.example.com.
@       IN      A       192.168.1.10
ns1     IN      A       192.168.1.10
www     IN      A       192.168.1.20
```

### Restart BIND:
```
sudo systemctl restart bind9
```

## 3. NAT (Network Address Translation)

NAT is typically configured using iptables in Linux.

### First, enable IP forwarding:
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

### To make this permanent, edit `/etc/sysctl.conf`:
```
net.ipv4.ip_forward=1
```

### Configure NAT with iptables:
```
# Clear existing rules
iptables -F
iptables -t nat -F

# Set default policies
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# Allow established connections
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allow internal network to access external network
iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT

# NAT configuration
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

# Allow incoming SSH (adjust as needed)
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

### This configuration:
- Clears existing rules
- Sets default policies
- Allows established connections
- Permits internal to external network access
- Sets up NAT
- Allows incoming SSH connections

### Save the iptables rules:
```
sudo iptables-save > /etc/iptables.rules
```

### To load these rules on boot, create a file `/etc/network/if-pre-up.d/iptables` with:

```
#!/bin/sh
iptables-restore < /etc/iptables.rules
```

### Make it executable:
```
chmod +x /etc/network/if-pre-up.d/iptables
```

This guide provides a basic setup for DHCP, DNS, and NAT on a Linux system. Remember to adjust IP addresses, interface names, and other specifics to match your network setup. Also, ensure you have the necessary permissions and consider security implications when configuring these services.
