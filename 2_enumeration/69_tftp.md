# 69\_TFTP

## Background

* Very old service that is similar to an FTP server.  However it operates over UDP protocol instead of TCP.

## Manual Enumeration

```text
tftp [IP] PUT [local file location].[extension]
```

```text
tftp [IP] GET [remote file location].[extension]
```

* Some older versions of Solaris allow you to download the remote passwd file.

  ```text
  tftp -i [IP] GET /etc/passwd
  ```

