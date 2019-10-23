# 79\_Finger

## Background

* Finger servers provide information about the users of their computers by opening and listening for incoming TCP connections on port 79. 
* Remote users wishing to obtain information about the user of a specific computer could do so by querying their machine's finger server listening on port 79. 
* Information typically included the user's full name, address, telephone number, title, job name, office location, telephone extension, etc. 
* Very old service.  If this is on a box, then the box is usually an outdated operating system.

## Manual Enumeration

```text
finger [user]@[domain].[com]
```

## Automated Enumeration

### Metasploit

* Auxiliary module that cycles through a pre-defined list of users to identify which users are valid.

  ```text
  auxiliary/scanner/finger/finger_users
  ```

  **Perl Script**

* [Finger-User-Enum](https://github.com/pentestmonkey/finger-user-enum)
* Identifies which users have logged into the system.
* In the results of the script, you can identify which users have logged in by identifying which ones have terminals \(pts/2\) with IP's associated with the user.

