# IP Routing

## 1. Fundamentals of IP Routing in Linux

IP routing is the process of forwarding IP packets from one network to another. In Linux, the kernel is responsible for routing decisions based on the routing table.

Key concepts:
- IP address
- Subnet mask
- Default gateway
- Routing table

## 2. The Linux Routing Table

The routing table is a data structure in the Linux kernel that stores routing information. You can view it using the `route` or `ip route` commands.

Example:
```
$ ip route show
default via 192.168.1.1 dev eth0 
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.100
```

## 3. Basic Routing Commands

- a) Adding a route:
```
ip route add 10.0.0.0/24 via 192.168.1.254
```

- b) Deleting a route:
```
ip route del 10.0.0.0/24
```

- c) Adding a default gateway:
```
ip route add default via 192.168.1.1
```

## 4. Network Interfaces

Linux treats network interfaces as the point where IP packets enter or leave the system. Common types include:
- Ethernet (eth0, eth1)
- Wireless (wlan0)
- Loopback (lo)

You can view and configure interfaces using the `ip link` and `ip addr` commands.

## 5. IP Forwarding

To use a Linux system as a router, you need to enable IP forwarding:

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

To make this permanent, edit `/etc/sysctl.conf`:
```
net.ipv4.ip_forward = 1
```

## 6. Policy-Based Routing

Linux supports policy-based routing, allowing you to make routing decisions based on criteria other than the destination address.

Key components:
- Multiple routing tables
- Rules for selecting tables

Example of creating a new routing table:
```
echo "200 custom" >> /etc/iproute2/rt_tables
ip route add default via 10.0.0.1 table custom
ip rule add from 192.168.1.0/24 table custom
```

## 7. Dynamic Routing Protocols

For larger networks, dynamic routing protocols are essential. Linux supports various routing daemons:

- Quagga: Supports OSPF, BGP, RIP
- BIRD: Lightweight routing daemon for IPv4 and IPv6
- FRRouting: Fork of Quagga with additional features

## 8. Netfilter and iptables

While primarily used for firewalling, iptables can also influence routing decisions:

- DNAT (Destination NAT) for port forwarding
- SNAT (Source NAT) for masquerading

Example of DNAT:
```
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.100:8080
```

## 9. Advanced Routing Features

- a) Equal-Cost Multipath (ECMP) Routing:
```
ip route add default equalize nexthop via 192.168.1.1 weight 1 nexthop via 192.168.1.2 weight 1
```

- b) Source-based routing:
```
ip route add 10.0.0.0/24 via 192.168.1.1 src 192.168.1.100
```

## 10. Troubleshooting and Monitoring

Essential tools for diagnosing routing issues:
- traceroute / tracepath
- ping
- mtr (My TraceRoute)
- tcpdump
- netstat / ss

Example of using tcpdump to monitor routing:
```
tcpdump -i eth0 icmp
```

## 11. IPv6 Routing

Most of the concepts apply to IPv6 as well, with some differences:
- Use of link-local addresses
- Neighbor Discovery Protocol (NDP) instead of ARP
- Different address notation

Example of adding an IPv6 route:
```
ip -6 route add 2001:db8::/64 via fe80::1 dev eth0
```

## 12. Kernel Tuning for Routing Performance

You can optimize the kernel for routing performance by adjusting sysctl parameters:

```
net.ipv4.ip_forward = 1
net.ipv4.conf.all.rp_filter = 1
net.ipv4.tcp_syncookies = 1
```

This guide covers the core concepts and practical aspects of IP routing in Linux. Would you like me to elaborate on any specific area or provide more examples?
