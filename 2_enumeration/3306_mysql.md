# 3306\_MySQL

## Background

When you attempt to connect to this port, you will generally see the following error because the MySQL DB is configured so only the root user is allowed to login from the local host IP \(127.0.0.1\).

* ERROR 1130 \(HY000\): Host '192.168.0.101' is not allowed to connect to this MySQL server.

## Enumeration

### NMap

```text
nmap -A -n -p 3306 [IP]
```

```text
nmap -A -n -PN --script:ALL -p 3306 [IP]
```

```text
nmap --script=mysql-databases.nse,mysql-empty-password.nse,mysql-enum.nse,mysql-info.nse,mysql-variables.nse,mysql-vuln-cve2012-2122.nse [IP] -p 3306
```

### Metasploit

```text
use auxiliary/scanner/mssql/mssql_ping
```

