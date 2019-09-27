# Background
- Used to resolve hostnames to IP addresses and vice versa. 
- Divulge DNS and mail server information for the domain it has authority over. 
- Zone transfer: Replicating the zone file from the master (authoritative) DNS server to a slave (secondary) DNS server.  The zone file contains a list of all the DNS names configured for that zone.  Zone transfers must be allowed for the internet to work but should be restricted to just allow authorized slave (secondary) DNS servers to perform them. 
- More important in internet-facing domains. Less important in small subnets as communication between subnet hosts relies on layer 2 ARP packets through MAC addresses.

# Manual Enumeration
1. Identifying the DNS and mail servers for a named domain: 
```
host –t ns [domain name] 
```
  - -t: Type 
  - ns: DNS server 
```
host –t mx [domain name] 
```
  - mx: Mail server 
2. Get the IP address of a named website (forward DNS lookup): 
```
host [website name] 
```
3. You can create a list of pre-pend names (www, ftp, mail, owa, proxy, router, etc.) for a domain to see if they exist for a named domain. 
```
host [pre-pend name].[domain name].com 
```
4. Find any website names that resolves from a given IP address (reverse DNS lookup): 
  - Only works if the DNS server is configured with PTR (pointer) records for the domain. 
  - This is helpful to make sure we have a complete population of valid IP addresses for a given IP range. 
```
host [IP address] 
```
```
nslookup
> server [target IP]
> [target IP]
```
  - ippsec:CronOS
- Generally have a script that automates the population of the IP address for a block of addresses. 
```
for ip in $(seq 155 190); do host 10.11.12.$ip; done | grep –v "not found" 
```
5. Attempt a zone transfer 
  - If the master (authoritative) DNS server is misconfigured, then any IP address can execute a zone transfer to get a full server listing for the domain. 
```
host –l [domain name] [DNS master server address] 
```
```
dnsrecon –d [domain name] -t axfr 
```
```
dig axfr @ [target IP] [domain name]
```
  - ippsec:CronOS
