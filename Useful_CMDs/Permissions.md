# SETUID / SETGID
- Each of these are a boolean value (0 or 1).  
- These two rights allow any user to execute the program with the rights of the owner or group, respectively.  It grants access to features requiring higher level permissions than those that a user would usually have.  
- If a program has a SETUID of root, then it runs systematically as root.  Penetration testers generally look for these programs as any flaws in them allows the testers to escalate their privileges in the environment.

# Directory Permissions
- Read: Gives the access to see the list of contents in the directory  
- Write: Allows creating or deleting files (not editing).  
- Execute: Allows the ability to cross through the directory to access it's contents (like using the cd command to cross into the directory to use other commands like cat and cp).  
- Note: If you have execute privileges but not read – you can cross into the directory if you know the exact name of the files / folders you're trying to access.  You won't have the ability to see any of the contents of the directory without knowing the exact name.

# General Permission Syntax

## Text Format
- Assign users with read, write, and execute.
```
U=rwx
U+rwx
```
- Remove read, write, and execute from the user.
```
U-rwx
```
- U: User owner of the file. 
- G: Group is owner of the file. 
- O: Other (not u or g) users (global).
- A: All of the above.

## Octal Format
- Note: You overwrite previous permissions when you use octal format as all permissions have to be re-defined each command entry.

### Normal Rights
- Read (4)
- Write (2)
- Execute (1)
-  Order determined by User, Group, Global (other).

### Special Rights
- A fourth digit representing:
  - SETUID (4)
  - SETGID (2)
  - Sticky Bit (1)
