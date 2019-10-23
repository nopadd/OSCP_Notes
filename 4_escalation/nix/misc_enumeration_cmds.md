# Misc\_Enumeration\_CMDs

## World-Writable Files / Directories

* General

  ```text
  find / -type f -perm -2 2>/dev/null | grep -v "^/proc/" 
  find / -perm -2 -type d 2>/dev/null | grep -v "^/proc/"
  ```

* World-writeable Folders

  ```text
  find / -writable -type d 2>/dev/null
  find / -perm -222 -type d 2>/dev/null
  find / -perm -o w -type d 2>/dev/null
  ```

* World-Executable Folders

  ```text
  find / -perm -o x -type d 2>/dev/null
  ```

* World-Writeable & Executable Folders

  find / \( -perm -o w -perm -o x \) -type d 2&gt;/dev/null

  \`\`\`

* World-Writeable Files

  ```text
  find / -xdev -type d \( -perm -0002 -a ! -perm -1000 \) -print
  ```

* Files w/ No Owners

  ```text
  find /dir -xdev \( -nouser -o -nogroup \) -print
  ```

## Files Modified / Accessed / Changed In Last 60 Minutes

```text
find / -type f -amin 60 -ls 2> /dev/null
find / -type f -mmin 60 -ls 2> /dev/null 
find / -type f -cmin 60 -ls 2> /dev/null
```

## Files w/ Interesting Extensions

```text
find / -type f -size +0 -iname "*.cfg" -o -iname "*.rtf" -o -iname "*.config" -o -iname "*.txt" -o -iname "*.c" -o -iname "*.pl" -o -iname "*.gz" -o -iname "*.bz2" -o -iname "*.7z" -o -iname "*.log" -o -iname "*.tar" -o -iname "*.tgz" -o -iname "*.sql" -o -iname "*.properties" -o -iname "*.xml" -ls 2> /dev/null
```

## Check Permissions on Sensitive Files

```text
find / -type f -size +0 -regex ".*\(shadow\|password\|passwd\|authorized_keys\|identity\|id_dsa\|id_rsa\|ssh\|rhosts\|htaccess\|htdigest\|svn.simple\).*" -ls 2>/dev/null
locate -e -L -i -q "*shadow" "*password" "*passwd" "*authorized_keys" "*identity" "*id_dsa" "*id_rsa" "*ssh" "*rhosts" "*htaccess" "*htdigest" "*svn.simple"
```

## Check SUDO Version For Vulnerabilities

```text
sudo -V
```

## Readable Mail From Users

```text
find /var/mail -readable -ls 2>/dev/null 
find /var/spool/mail -readable -ls 2>/dev/null
```

## Configuration Files Current User Has Write Access

* Owner

  ```text
  ls -alR /etc/ | grep -v '^l' | awk '$1 ~ /^..w/' 2>/dev/null
  ls -alR /etc/ | grep -v '^l' | awk '$1 ~ /w.$/' 2>/dev/null
  ```

* Group

  ```text
  ls -alR /etc/ | grep -v '^l' | awk '$1 ~ /^.....w/' 2>/dev/null
  ```

## Configuration Files Current User Has Read Access

```text
find /etc/ -readable -type f 2>/dev/null
```

## Log Files Current User Has Read Access

```text
find /var/log -readable -type f 2>/dev/null
```

## List Unmounted File Systems w/ Sensitive Files

```text
cat /etc/fstab 
cat /etc/mtab 
mount 
df -h
```

## List Mounted Printers

```text
lpstat -a
```

