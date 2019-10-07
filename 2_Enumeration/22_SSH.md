# Background
- Most versions of SSH aren't vulnerable to remote code execution except some really old versions.
- The format of SSH banner grabbing results: SSH-protoversion-softwareversion (space) comments.

# Banner Grabbing
```
nc [IP] 22
```
```
telnet [IP] 22
```

# Fingerprint OS (ippsec:Shocker)
- The version number on the SSH application that is grabbed from NMap service scanning is much more specific than service scanning on other ports like HTTP(s).  This will allow us to identify the OS distro as well as version and patch level.
1. Perform an Nmap service scan on SSH.  Syntax of the format output is SSH Application : SSH App Version : OS Distro : OS Distro Patch Level.
2. Use launchpad.net to match the SSH App, OS distro, and patch level to identify the last update date (Uploaded by.... on \[date]).
