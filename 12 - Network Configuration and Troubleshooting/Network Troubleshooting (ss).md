# network troubleshooting using the `ss` (Socket Statistics)

## 1. Introduction to `ss`:
`ss` is a powerful utility for investigating sockets. It replaces the older `netstat` command and provides more detailed information about network connections.

## 2. Basic usage:
To display all connections:
```
ss
```

## 3. Common options:
   - `-t`: Show TCP sockets
   - `-u`: Show UDP sockets
   - `-l`: Show only listening sockets
   - `-a`: Show both listening and non-listening sockets
   - `-n`: Don't resolve service names
   - `-p`: Show process using the socket

## 4. Displaying TCP connections:
```
ss -t
```

## 5. Showing listening sockets:
```
ss -l
```

## 6. Combining options:
To show listening TCP sockets with process information:
```
ss -tlp
```

## 7. Filtering connections:
   - By state:
     ```
     ss state established
     ```
   - By port:
     ```
     ss sport = :80
     ```
   - By IP address:
     ```
     ss dst 192.168.1.1
     ```

## 8. Advanced filtering:
Use expressions for complex filters:
```
ss -t '( dport = :ssh or sport = :ssh )'
```

## 9. Displaying socket statistics:
```
ss -s
```

## 10. Checking for specific issues:
    - High number of TIME_WAIT connections:
      ```
      ss -t state time-wait | wc -l
      ```
    - Connections in SYN-SENT state (potential connectivity issues):
      ```
      ss -t state syn-sent
      ```

## 11. Investigating socket buffers:
```
ss -tm
```

## 12. Displaying timer information:
```
ss -to
```

## 13. Checking for UNIX domain sockets:
```
ss -x
```

## 14. Combining with other tools:
- Use with `grep` for specific searches:
     ```
     ss -tuln | grep :80
     ```
- Pipe to `less` for easier navigation:
     ```
     ss -tuna | less
     ```

## 15. Troubleshooting steps:
- a. Check for listening services:
       ```
       ss -tlnp
       ```
- b. Verify established connections:
       ```
       ss -tnp state established
       ```
- c. Look for connection attempts:
       ```
       ss -tnp state syn-sent
       ```
- d. Investigate connection closures:
       ```
       ss -tnp state time-wait
       ```
- e. Check for any unusual states or high connection counts

## 16. Performance considerations:
    - Use `ss -i` to display TCP internal information
    - Monitor retransmission rates and window sizes

## 17. Security checks:
    - Look for unexpected listening ports
    - Check for connections from unknown IP addresses

## 18. Debugging application issues:
    - Use `-p` option to correlate sockets with processes
    - Investigate socket states for hung connections

## 19. Network tuning:
    - Use socket statistics to identify bottlenecks
    - Adjust system parameters based on observed behavior

## 20. Scripting with `ss`:
    - Use in shell scripts for automated monitoring
    - Combine with `awk` or `sed` for custom output formatting

Remember that some `ss` commands may require root privileges to access all information. Always use caution when interpreting network data, especially in production environments.
