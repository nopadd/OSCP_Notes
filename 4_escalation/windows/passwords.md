# Passwords

## Storage Location

1. Windows stores hashes of the passwords in the following location.  Users with low privleges can't access it unless the permissions are missconfigured \(should check\).

   ```text
   C:\Windows\System32\config\SAM
   ```

2. If we can read the hashes here, then we should grab the following file to for hash cracking.

   ```text
   C:\Windows\System32\config\SYSTEM
   ```

3. Use samdump2 to crack the hashes

   ```text
   samdump2 [SYSTEM file] [SAM file]
   ```

   * This command will generate a list of users and their hashes which can be cracked with PW cracking tools or use in Pass The Hash techniques.

## Helpful Reference

[https://blog.ropnop.com/practical-usage-of-ntlm-hashes/](https://blog.ropnop.com/practical-usage-of-ntlm-hashes/)

