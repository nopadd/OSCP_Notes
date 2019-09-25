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
