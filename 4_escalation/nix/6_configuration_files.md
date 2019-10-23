# 6\_Configuration\_Files

## General

Generally stored under the /etc/ folder.

## Attack Vector

1. General methodology is to identify config files you have write access to and then see if you can abuse that access.  

   ```text
   find / -perm -o+w -type f 2>/dev/null | grep -v '/sys\|proc'
   ```

   * Find files that you have write access to. Focus on the ones in the /etc/ folder. 

2. Find configuration files in /etc/ which we can potentially access and change. 

   ```text
   ls -aRl /etc/ | awk '$1 ~ /^.*w.*/' 2>/dev/null     # Anyone 
   ls -aRl /etc/ | awk '$1 ~ /^..w/' 2>/dev/null       # Owner 
   ls -aRl /etc/ | awk '$1 ~ /^.....w/' 2>/dev/null    # Group 
   ls -aRl /etc/ | awk '$1 ~ /w.$/' 2>/dev/null        # Other 
   find /etc/ -readable -type f 2>/dev/null               # Anyone 
   find /etc/ -readable -type f -maxdepth 1 2>/dev/null   # Anyone
   ```

