# 23\_Telnet

## Background

* Telnet is considered insecure mainly because it does not encrypt its traffic.
* Multiple versions of Telnet have remote code execution vulnerabilities in MSF.

## Banner Grabbing

```text
telnet [IP]
```

* Common Banner Lists:
  * BannerSolaris 8/SunOS 5.8
  * Solaris 2.6/SunOS 5.6  
  * Solaris 2.4 or 2.5.1/Unix\(r\) System V Release 4.0 \(hostname\)  
  * SunOS 4.1.x/SunOS Unix \(hostname\)  
  * FreeBSD/FreeBSD/i386 \(hostname\) \(ttyp1\)  
  * NetBSD/NetBSD/i386 \(hostname\) \(ttyp1\)  
  * OpenBSD/OpenBSD/i386 \(hostname\) \(ttyp1\) 
  * Red Hat 8.0/Red Hat Linux release 8.0 \(Psyche\)  
  * Debian 3.0/Debian GNU/Linux 3.0 / hostname  
  * SGI IRIX 6.x/IRIX \(hostname\)  
  * IBM AIX 4.1.x/AIX Version 4 \(C\) Copyrights by IBM and by others 1982, 1994.IBM AIX 4.2.x or 4.3.x/AIX Version 4 \(C\) Copyrights by IBM and by others 1982, 1996.Nokia IPSO/IPSO \(hostname\) \(ttyp0\)  
  * Cisco IOS/User Access VerificationLivingston ComOS/ComOS - Livingston PortMaster  

