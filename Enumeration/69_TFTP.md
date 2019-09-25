# Background
- Very old service that is similar to an FTP server.  However it operates over UDP protocol instead of TCP.

# Manual Enumeration
```
tftp [IP] PUT [local file location].[extension]
```
```
tftp [IP] GET [remote file location].[extension]
```
- Some older versions of Solaris allow you to download the remote passwd file.
```
tftp -i [IP] GET /etc/passwd
```
