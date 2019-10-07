# Background
Common UNIX Printing System (CUPS) has become the standard for sharing printers on a linux-network.

# Enumeration
- Go to http://[IP address]:631/printers and see the CUPS version in the title bar of the browser.
```
test cups-config --version 
```
