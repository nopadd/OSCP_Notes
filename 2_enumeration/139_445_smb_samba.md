# 139\_445\_SMB\_Samba

## Background

* Samba is a service that enables the user to share files with other machines 
* It has interoperatibility, which means that it can share stuff between linux and windows systems. 
  * A windows user will just see an icon for a folder that contains some files. Even though the folder and files really exists on a linux-server.

## Enumeration

### SMBClient

* For linux-users you can log in to the smb-share using smbclient, like this:  

  ```text
  smbclient -L [IP]
  ```

  ```text
  smbclient //[IP]/tmp
  ```

  ```text
  smbclient \\\\[IP]\\ipc$ -U [user name]
  ```

  ```text
  smbclient //[IP]/ipc$ -U [user name]
  ```

* If you don't provide any password, just click enter, the server might show you the different shares and version of the server. This can be useful information for looking for exploits. There are tons of exploits for smb.

### PSExec

* You need valid credentials to use PSExec to connect. 

  ```text
  use exploit/windows/smb/psexec
  ```

### NMap Scripts

```text
nmap -p 139,445 [IP]
```

* List available NSE Scripts for SMB:

  ```text
  ls -l /usr/share/nmap/scripts/smb*
  ```

  **RPC Client**

* Connect with a null-session. That is, without a user. This only works for older windows servers.

  ```text
  rpcclient -U "" [IP]
  ```

* Once connected, you can enter the following commands for enumeration.
  * srvinfo  
  * enumdomusers  
  * getdompwinfo  
  * querydominfo  
  * netshareenum  
  * netshareenumall

