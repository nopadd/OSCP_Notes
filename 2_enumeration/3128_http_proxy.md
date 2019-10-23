# 3128\_HTTP\_Proxy

## Background

* This is a HTTP proxy server that is set up on the host that, if missconfigured, allows any external attacker to proxy into the target host and interact with it as if they were the localhost.
* This allows attackers to interact with otherwise closed or filtered ports because they are operating as the localhost during scanning and interaction.

## Enumeration

* Goal is to understand what additional ports and services are available to us on the target host if we navigate to the target host through the proxy.

### Metasploit

* There is a Metasploit auxillary module that can automatically scan the proxy on the target to identify what ports and services are available if navigating through the proxy.

  ```text
  auxillary/scanner/http/squid_pivot_scanning
  ```

### Spose.py

* This is a python3 script that emulates what the auxillary module from Metasploit does but through a custom python3 script.

  ```text
  git clone https://github.com/aancw/spose.git
  python3 spose.py --proxy http://[IP]:[port] --target [IP]
  ```

