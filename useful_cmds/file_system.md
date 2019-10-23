# File\_System

## Background

* Organized as a single \(ONE\) hierarchical structure starting at the root directory \(/\) with sub-directories stemming off of the root directory.   
* One storage disk becomes the root disk and the others are mounted on directories within the root hierarchy.  The other disks are available under 'mount points'.   
* The kernel translates between this naming file system and the physical storage location on the disk.

## Standard Top-Level Directories

* /bin/: Basic programs
* /boot/: Kernel and other files required for its early boot process
* /dev/: Device files   
* /etc/: Configuration files   
* /home/: User’s personal files   
* /lib/: Basic libraries   
* /media/\*: Mount points for removable devices \(CD-ROM, USB keys, and so on\)   
* /mnt/: Temporary mount point   
* /opt/: Extra applications provided by third parties   
* /root/: Administrator’s \(root’s\) personal files   
* /run/: Volatile runtime data that does not persist across reboots \(not yet included in the FHS\)   
* /sbin/: System programs   
* /srv/: Data used by servers hosted on this system   
* /tmp/: Temporary files \(this directory is often emptied at boot\)   
* /usr/: Applications
  * This directory is further subdivided into bin, sbin, lib according to the same logic as in the root directory.
  * /usr/share/: Contains architecture-independent data.
  * /usr/local/directory: Meant to be used by the administrator for installing applications manually without overwriting files handled by the packaging system \(dpkg\). 
* /var/: Variable data handled by daemons. This includes log files, queues, spools, and caches.   
* /proc/ and /sys/: Specific to the Linux kernel \(and not part of the FHS\). They are used by the kernel for exporting data to user space.

## User's Home Directories

* Referred to as '~'.  You can use ~ in commands and the interpreter will automatically substitute the correct user directory in place of the ~
* The correct user directory is stored in the HOME Environmental variable and the usual value is /home/\[user\]/.   
* Configuration files / directories for user applications are usually stored under the user's directory as a hidden file \(prefix of .\) - usually called 'dotfiles'. 

