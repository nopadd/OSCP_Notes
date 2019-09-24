# NMap
Can be used for scanning a range of IP's.
```nmap -sP -n -sn [IP range]```
- -sP: Ping sweep an IP range.
- -sn: No port scan, just does host discovery.
- -n: Disable DNS resolution.

# Ping
Can only be used for one host at a time and used ICMP message type 8.
```ping [IP]```
- -l: Set the ping packet size.
- -a: Resolve IP to hostname.
- -s: Timestamp.
## ICMP Reply Types
- 0: Echo Reply, answer to Type 8 Request 
- 3: Destination Unreachable 
  - 0: Network unreachable 
  - 1: Host unreachable 
  - 2: Protocol (ICMP) unreachable 
  - 3: Port unreachable 
  - 9: Network Administratively prohibited 
  - 10: Host administratively prohibited 
  - 13: Communication administratively prohibited (firewall blocking ICMP Type 8 requests). 
- 5: Redirect 
- 11: Time exceeded - took too long to be routed to the destination. 
