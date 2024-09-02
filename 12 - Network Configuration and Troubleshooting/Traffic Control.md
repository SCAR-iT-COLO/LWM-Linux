# Internet Traffic Control

## 1. Introduction to Traffic Control (TC)

Traffic Control (TC) is a set of tools and mechanisms in Linux that allow you to shape, schedule, police, and prioritize network traffic. It's part of the Linux kernel's networking stack and provides powerful capabilities for managing network bandwidth and latency.

## 2. Key Concepts

- a) Queueing Disciplines (qdisc):
A qdisc is a scheduler that controls how packets are sent or received on a network interface. There are two types:
- Classless: Simple, single-queue disciplines
- Classful: More complex, can contain multiple classes of traffic

- b) Classes:
Within classful qdiscs, classes allow you to categorize traffic and apply different rules to each category.

- c) Filters:
Used to classify packets into different classes based on various criteria.

- d) Tokens and Buckets:
Many TC algorithms use the concept of tokens and buckets to control traffic rates.

## 3. Common Queueing Disciplines

a) pfifo_fast: Default qdisc, a simple FIFO queue with three bands for prioritization.
b) tbf (Token Bucket Filter): Limits traffic to a specified rate.
c) htb (Hierarchical Token Bucket): Allows complex hierarchical class-based traffic control.
d) sfq (Stochastic Fairness Queueing): Attempts to fairly distribute traffic among flows.
e) netem: Network emulator for testing, can introduce delay, loss, duplication, and more.

## 4. Basic TC Commands

The tc command is the primary tool for configuring Traffic Control. Basic syntax:

```
tc [OPTIONS] OBJECT { COMMAND | help }
```

OBJECT can be:
- qdisc (Queueing discipline)
- class
- filter

Common COMMANDS include:
- add
- del
- change
- show (or list)

## 5. Examples of TC Usage

- a) Setting up a simple rate limiter:
```
tc qdisc add dev eth0 root tbf rate 1mbit burst 32kbit latency 400ms
```

- b) Creating a hierarchical setup with HTB:
```
# Create root qdisc
tc qdisc add dev eth0 root handle 1: htb default 30

# Add classes
tc class add dev eth0 parent 1: classid 1:1 htb rate 100mbit
tc class add dev eth0 parent 1:1 classid 1:10 htb rate 50mbit ceil 100mbit
tc class add dev eth0 parent 1:1 classid 1:20 htb rate 30mbit ceil 100mbit
tc class add dev eth0 parent 1:1 classid 1:30 htb rate 20mbit ceil 100mbit

# Add filters to classify traffic
tc filter add dev eth0 protocol ip parent 1:0 prio 1 u32 match ip dport 80 0xffff flowid 1:10
tc filter add dev eth0 protocol ip parent 1:0 prio 1 u32 match ip sport 22 0xffff flowid 1:20
```

## 6. Advanced Features

a) Ingress qdisc: Control incoming traffic
b) Shaping vs. Policing: Shaping buffers traffic, policing drops excess
c) Classifying with iptables: Use MARK target to classify packets
d) Handling of TCP vs UDP traffic

## 7. Monitoring and Debugging

a) Use `tc -s qdisc show dev eth0` to see statistics
b) tcpdump can help analyze traffic patterns
c) iftop or nethogs for real-time bandwidth usage monitoring

## 8. Best Practices

a) Start simple and gradually increase complexity
b) Test configurations thoroughly before deploying
c) Consider the impact on application performance
d) Document your TC setup for future reference

## 9. Integration with Other Systems

a) Combine with QoS markings (e.g., DSCP) for end-to-end traffic management
b) Use with firewalls for comprehensive network control
c) Automate TC configurations with scripts or configuration management tools

## 10. Limitations and Considerations

a) Complex setups can impact CPU usage
b) Some features may not work with all network drivers
c) Virtual environments may have limitations or require special configurations
