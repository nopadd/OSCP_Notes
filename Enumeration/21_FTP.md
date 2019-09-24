# Background
- Remember binary vs. ASCII mode.  If you choose the wrong mode for the file type, it will become corrupted.
  - Binary: To upload a binary file type to an FTP server, you have to be in binary mode.
  - ASCII: To upload a text file to an FTP server, you have to be in ASCII mode.
  
# Enumeration Steps

## Banner Grabbing
Connect to the FTP server to enumerate the software and version.
```
ftp [IP]
```
```
nc [IP] 21
```
  - Note that NetCat doesn't allow all types of commands.  The FTP client is more preferred if available.
