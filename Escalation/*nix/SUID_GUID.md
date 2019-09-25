# Background
- SUID = Set User ID 
- Allows users to execute a file with the permissions of a specified user. 
- It is represented by an 's' in the execute bit of a permission list for the first 3 octals (user section).
```
Rws rwx rwx
```
- The owner user of the file is the user that will be executing the at the direction of the account using the SUID functionality.

# Find SUID Files
```
find / -perm -u=s -type f 2>/dev/null
```

# Find GUID Files
```
find / -perm -g=s -type f 2>/dev/null
```

# General Search For SUID/GUID Files in Common Places
Common places include: /bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, /usr/local/sbin and any other *bin.
```
for i in `locate -r "bin$"`; do find $i \( -perm -4000 -o -perm -2000 \) -type f 2>/dev/null; done
```
```
find / -perm -g=s -o -perm -4000 ! -type l -maxdepth 3 -exec ls -ld {} \; 2>/dev/null
```
