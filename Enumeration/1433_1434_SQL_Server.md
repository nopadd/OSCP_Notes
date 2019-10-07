# Background
- TCP port that is used for clients to connect to the SQL DB on the host for querying and updating data. 
- Having this open in combination with port 80/443 with a website being hosted on the target is a strong indication that the DB behind the website is a SQL DB and the website could be vulnerable to SQL injection attacks.

# Enumeration

## Metasploit
```
MSF > use auxiliary/scanner/mssql/mssql_ping
```

## SQLPing
```
sqlping [IP]
```

## SQSH
```
sqsh -S [IP] -U [username]
```
