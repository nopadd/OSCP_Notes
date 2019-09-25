# Background
- Server Message Block (SMB) for Windows OS that has a history of being insecure leakage of NetBIOS information over the years.  It is likely an enumeration vector for any Windows OS 7 or older. 
- The default OS using SMB is Windows, but there was a version ported over to Unix called Samba. 
- Lists all of the connected network resources for an individual host. 
- Version listing 
  - SMB1: Windows 2000, XP, 2003 
    - This was the version susceptible to eternal blue exploit.  
  - SMB2: Vista SP1, 2008 
  - SMB2.1: 7 and 2008 R2 
  - SMB3: 8 and Windows 2012 
- Listens on TCP port 139 and 445 but it also listens on a number of UDP ports too. 
- NetBIOS codes and suffixes 
  - For unique names: 
    - 00: Workstation Service (workstation name) 
    - 03: Windows Messenger service 
    - 06: Remote Access Service 
    - 20: File Service (also called Host Record) 
    - 21: Remote Access Service client 
    - 1B: Domain Master Browser – Primary Domain Controller for a domain 
    - 1D: Master Browser 
  - For group names: 
    - 00: Workstation Service (workgroup/domain name) 
    - 1C: Domain Controllers for a domain 
    - 1E: Browser Service Elections 
- Null Sessions 
  - Certain versions (SMB1) / configurations allow for null sessions which menas an unauthenticated NetBIOS session between 2 computers can be established over this service. 
  - This allows the connecting computer to dump large amounts of information (password policies, usernames, group names, machine names, user and host SID's).

# Manual Enumeration

## Initial enumeration 
```
nbtscan –r [IP]
```
  - NetBIOS Name: Hostname of the computer
```
nmblookup -A [IP]
```
  - This displays the NetBIOS names and prefixes for a specific IP of interest that you see from the nbtscan results.

## Enum4linux
- Enumerates a lot of services including SMB and attempts null session authentication to extract information. 
```
enum4linux -a [IP]
```
## NMap NSE Scripts
- Contained in /usr/share/nmap/scripts/smb location. 
- Useful ones include 'smb-vulns' and 'smb-os-discovery' 
```
nmap –p 135, 445 –script=[script name] [IP]
```
```
nmap --script=smb-enum-shares.nse,smb-ls.nse,smb-enum-users.nse,smb-mbenum.nse,smb-os-discovery.nse,smb-security-mode.nse,smbv2-enabled.nse,smb-vuln-cve2009-3103.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms17-010.nse, smb-vuln-ms10-061.nse,smb-vuln-regsvc-dos.nse,smbv2-enabled.nse $IP -p 445
```

## SMBMAP 
- SMBMap allows users to enumerate samba share drives across an entire domain. List share drives, drive permissions, share contents, upload/download functionality, file name auto-download pattern matching, and even execute remote commands.  
- General enumeration of file shares:
```
Smbmap -H [IP]
```

## RPCclient (authentication required)
- Allows for interaction with Windows machines from Unix boxes. 
```
rpcclient -U "[user name]" [IP]
```
  - Can do a null session with username of "" and -N option. 
### Commands to enter once authenticated:  
- srvinfo 
- enumdomusers 
- getdompwinfo 
- querydominfo
- netshareenum 
- netshareenumall 
```
smbclient -L [IP]
```
```
Queryuser [userid] 
```

## Null Session  
### Windows 
```
>net use \\[IP]\ipc$ "" /u:""  
>net view \\[IP]
```
### Linux
- See SMBClient commands below. 

## Smbclient  
- Client that can ‘talk’ to an SMB/CIFS server. It offers an interface similar to that of the FTP program. Operations include things like getting files from the server to the local machine, putting files from the local machine to the server, retrieving directory information from the server and so on.
```
smbclient -L //[IP]
```
```
smbclient //[IP]/ipc$ -U [user name]
```
  - Sometimes anonymous logins are allowed, which is a –U "" syntax.

## Enumerate RID's
### Metasploit 
```
use auxiliary/scanner/smb/smb_lookupsid
```
### Python
```
python /usr/share/doc/python-impacket-doc/examples 
/samrdump.py [IP]
```
### RIDEnum 
```
ridenum.py [IP] 500 50000 dict.txt 
```
