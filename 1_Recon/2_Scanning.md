# Quick / Limited Scanning
- TCP Scan
```
nmap -sC -sV -vv -oA [file] [IP]
```
- UDP Scan
```
nmap -sU -sV -vv -oA [file] [IP]
```

# Long / Noisy Scanning
- Faster method:
  1. Identify open ports from a full scan.
    ```
    nmap -p- -T4 [IP]
    ```
  2. Run a versioning and safe scripts scan on the open ports.
    ```
    nmap -p [port listing] -sC -sV [IP]
    ```
- Slower method:
  1. Full TCP scan with versioning and safe scripts.
    ```
    nmap -sT -sV -sC -O -vv -p- [IP]
    ```
  2. Full UDP scan with versioning and safe scripts.
    ```
    nmap -sU -sV -sC -O -vv -p- [IP]
    ```
- Full Windows Scan:
  ```
  nmap -W -sV -sC -O -vv -p- [IP]
  ```

# Nmap Flags
## s_: Scan Types 
- Primary 
  - -sT: TCP scan - default and only identifies TCP ports that are open. 
  - -sW: Windows scan. 
  - -sU: UDP scan - identifies only UDP ports that are open. 
    - Note this is not done by default unless indicated with this option. 
  - -sV: Versioning scanning - banner grabs all TCP services during scanning. 
  - -sC: Script scanning with default scripts. 
    - Available scripts are located at /usr/share/nmap/scripts 
    - Help on a script: #nmap --script-help [script name/category] 
    - Run an individual script against an IP address
      - 'nmap –script=[script name] [IP address]'
- Secondary 
  - -sS: SYN scan - stealth scan with a handshake of SYN-SYN/ACK-RST.  No TCP connection established. 
  - -sN: Null Scan - no flags set AKA inverse TCP. 
    - Doesn't work on Windows machines. 
  - -sX: XMAS Scan - all flags set. 
    - Doesn't work on Windows machines. 
  - -sO: Protocol Scan. 
## p_: Ping Types
- Reference the [1_Discovery](https://github.com/neogeo56/OSCP_Notes/blob/master/Recon/1_Discovery.md) page.
## -o_: Output Types 
- -oN: Normal output 
- -oX: XML output 
- -oA: Outputs to all formats 
## T_: Scan Speed 
  - -T1: Slowest and best for stealth 
  - -T3: Normal - default 
  - -T5: Fastest 
## Other 
  - Ports 
    - -p: [port number(s)] 
      - Scans most common 1,000 automatically. 
  - -p-: Scan all ports 
  - --traceroute 
    - -O: Attempt OS fingerprinting 
    - -A: Enables OS fingerprinting, traceroute, versioning, and script scanning. 
    - -vv: Very verbose output.
