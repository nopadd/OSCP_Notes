# 2\_Daemons

## Programs in Home Directories

### Background

* This is a very common spot for unique scripts / binaries / programs / notes to be found for further enumeration.
* If we can get command injection into a custom script / binaries / programs:
  * A quick-win is to have the elevated account change the permissions of the /bin/dash binary to a sticky bit.  This way normal users can execute /bin/dash to have an effective ID of root. \(ippsec:SolidState\)

    ```text
    chmod 4755 /bin/dash
    ```

  * The other standard option is a one-liner reverse [shell](https://github.com/neogeo56/OSCP/tree/master/Shells).

### Attack Vector

```text
ls -lat ~/
```

## Programs Running As Different Users

The idea here is that if specific service is running as root and you can make that service execute commands you can execute commands as root. Look for webserver, database or anything else like that. A typical example of this is mysql. 1. Check which processes are running as root.

```text
ps aux | grep 'root' 
ps –ef | grep 'root' 
cat /etc/services
```

1. If there's a different user that has an interactive shell available when looking at /etc/passwd/, then it could be valuable to identify if there are any services running as that user. Just substitue that username in place of root in the above commands. \(Vulnhub: Temple of Doom\)

## Cron Job

### Background

* Tasks or programs that are run on a set schedule on the operating system.  
* Cron jobs run with the permissions of the owner of it unless otherwise specified. 
* User cron jobs \(non-privileged users\) are separate from the system/root cron jobs.
* Important file locations:
  * The system/root level tasks are stored in the /etc/crontab file. The Cron Jobs in the file will be executed as root. 
  * The system/root crontab file is generally viewable by everyone, but not writeable.

### Identify Scheduled Cron Jobs

```text
crontab -l 
ls -alh /var/spool/cron 
ls -al /etc/ | grep cron 
ls -al /etc/cron* 
cat /etc/cron* 
cat /etc/at.allow 
cat /etc/at.deny 
cat /etc/cron.allow 
cat /etc/cron.deny 
cat /etc/crontab 
cat /etc/anacrontab 
cat /var/spool/cron/crontabs/root
```

### Attack Vector

Look for jobs run as root and see if any of them are executing scripts / programs that have permissions missconfigured for us to edit the script / program.

* Importing libraries that we have access to.
* Using commands that don't have the full binary path specified.
* Using other programs or binaries we can edit.

## Reverse Engineering \(ippsec=Irked\)

1. You can get a binary off of the target box and onto the attacker box with reverse engineering tools by using base64 encoding.

   ```text
   base64 -w0 [target binary file]
   ```

2. Copy the base64 encoding from the target machine to your attacker machine and save it to a text file.
3. Decode the base64 on your attacker machine to get a replica of the binary.

   ```text
   base64 -d [binary base64 text file] > [name of of the output file to be created]
   ```

4. Use STRACE / LTRACE / Ghidra on the binary file.
   * Create new project.
   * Click on Ghidra code browser button in the tool chest.
   * File -&gt; Import File -&gt; Source Code File.
   * Format: ELF
   * Language: x86 Default
   * Analyze: Select all options.
   * Symbol Tree Ribbon -&gt; Functions -&gt; Main
   * Look at the decompiler to see the source code.

## User Installed Software

* Has the user installed some third party software that might be vulnerable? Check it out. If you find anything google it for exploits. 
* Common locations for user installed software 

  ```text
  /usr/local/ 
  /usr/local/src 
  /usr/bin/
  /sbin/
  /usr/local/bin 
  /opt/ 
  /home 
  /var/ 
  /usr/src/
  ```

* Debian 

  ```text
  dpkg -l
  ```

  * CentOS, OpenSuse, Fedora, RHEL 

    ```text
    rpm -qa (CentOS / openSUSE )
    ```

* OpenBSD, FreeBSD 

  ```text
  pkg_info
  ```

## Services Only Available From Inside

### Background

* It might be that case that the user is running some service that is only available from that host. You can't connect to the service from the outside.
* These services might be running as root, or they might have vulnerabilities in them. They might be even more vulnerable since the developer or user might be thinking "since it is only accessible for the specific user we don't need to spend that much of security".

### Attack Vector

1. Check the netstat and compare it with the nmap-scan you did from the outside. Do you find more services available from the inside? 

   ```text
   netstat –anlp 
   netstat –ano 
   netstat -antup
   ```

2. If so there might be [Port Knocking](https://github.com/neogeo56/OSCP_Notes/blob/master/Enumeration/0_Port_Knocking.md) opportunities to open up a service to the outside or help inform unique daemons / processes / binaries to investigate further.

## Wildcards

### Background

* Wildcard character can be used to represent one or more other characters. 
* One example is the \* character. 
  * The \* character can represent zero or multiple characters in a string. 
* Bash will use wildcard characters to match file names and content.

### Attack Vector

* If a wildcard is used in a daemon command then there is a good chance that we can create a new program that will be interrperated as an argument for the command used in the daemon. 
* Example 
  * Daemon command: tar -czf /mnt/drive1/backup.tar.gz \* 
  * New malicious program: touch /home/user/files/--checkpoint-action=exec=sh pwn.sh 
    * This will get interperated as a "checkpoint action" argument for the daemon command and then execute our shell program as root.

## Tar Binary

### Background

* Standard binary used for compressing files into various compression formats.  

### Attack Vector

* If this binary is used to extract already compressed files through a program running as root then we can exploit it because tar inherits the permissions of the original file when it extracts the file.  
* Create a root shell program on the attacker machine that is a SETUID as root with a sticky bit for all users to execute and change the owner user and group to root.  
* Compress the file on the attacker machine with tar.  
* Transfer the file over to the target and have the target program with tar extraction action execute on our compressed SETUID root shell program.
* When the program extracts our file, it will be owned by user and group of root \(on the target machine\) with a sticky bit set for any user to execute the root shell program and drop into a root shell.

## Start-up Scripts

### Background

* Linux start-up scripts are generally located in /etc/init.d. 
* Other locations could be /etc/rc.d, /etc/rc.d/init.d, or /etc/init. 
* Some scripts are default with the operating system and some are user created. 

### Attack Vector

* Determine which start-up scripts you have write access to and then insert malicious commands to be executed upon boot of the machine. 

  ```text
  find / -perm -o+w -type f 2>/dev/null | grep -v '/sys\|proc'
  ```

## Mongo DB \(ippsec=Node\)

* If the DB is missconfigured, you can execute commands from the DB as the user who runs the DB service \(generally root\).
* Connect to the Mongo DB \(requires credentials\).

  ```text
  mongo -p -u [user] [mongo DB to connect to]
  ```

* Inject commands.

  ```text
  Db.tasks.insert ( { "cmd" : "commands to issue; another command to issue;" } )
  ```

  * Everything in Mongo DB is JSON formatted.

