# 25\_SMTP

## Background

* Simple Mail Transfer Protocol listens on TCP port 25. 
* Mail servers host this server on their box to allow connections from clients.  If misconfigured, it can be used to enumerate network users or the mail server host. 
* SMTP is a server to server service. The user receives or sends emails using IMAP or POP3. Those messages are then routed to the SMTP-server which communicates the email to another server. 
* The SMTP-server has a database with all emails that can receive or send emails. 
* We can use SMTP to query that database for possible email-addresses. 
* Note that we cannot retrieve any emails from SMTP. We can only send requests to it to enumerate the database that is stored with that service. 
* Communication is in clear text unless the TLS option is enabled \(not default\).
* If this port with other mail-type ports are open \(25, 110, 119\) - then we can likely run a local mail client to interact with these services more natively.
* Here are the documentations for SMTP: 
  * [https://cr.yp.to/smtp/vrfy.html](https://cr.yp.to/smtp/vrfy.html)  
  * [http://null-byte.wonderhowto.com/how-to/hack-like-pro-extract-email-addresses-from-smtp-server-0160814/](http://null-byte.wonderhowto.com/how-to/hack-like-pro-extract-email-addresses-from-smtp-server-0160814/)  
  * [http://www.dummies.com/how-to/content/smtp-hacks-and-how-to-guard-against-them.html](http://www.dummies.com/how-to/content/smtp-hacks-and-how-to-guard-against-them.html)  
  * [http://pentestmonkey.net/tools/user-enumeration/smtp-user-enum](http://pentestmonkey.net/tools/user-enumeration/smtp-user-enum)  
  * [https://pentestlab.wordpress.com/2012/11/20/smtp-user-enumeration/](https://pentestlab.wordpress.com/2012/11/20/smtp-user-enumeration/)

## Manual Enumeration

1. You can interact with this service through a NetCat or Telnet session.

   ```text
   nc -nv [IP] 25
   ```

   ```text
   telnet [IP] 25
   ```

2. Once connected, you can issue the following commands to enumerate the network users and/or mail server host.
   * VRFY: Asks the server to verify an email address or username. 
   * EXPN: Asks the server for membership of a mailing list. 
   * HELO: Primarily used for social engineering by sending spoofed emails.
     * Test a mail spoof \(used for social engineering\) 

       ```text
       #HELO [anything] MAIL FROM: [spoofed_address] RCPT TO: [valid_mail_account] DATA . QUIT
       ```

     * Mail Relay Test through interactive session \(used for Social Engineering\) 

       ```text
       #HELO [anything]
       ```

       * Identical to/from - mail from: [nobody@domain](mailto:nobody@domain) rcpt to: [nobody@domain](mailto:nobody@domain)  
       * Unknown domain - mail from: [user@unknown\_domain](mailto:user@unknown_domain)  
       * Domain not present - mail from: [user@localhost](mailto:user@localhost)  
       * Domain not supplied - mail from:   
       * Source address omission - mail from: &lt;&gt; rcpt to: [nobody@recipient\_domain](mailto:nobody@recipient_domain)  
       * Use IP address of target server - mail from: [user@IP\_Address](mailto:user@IP_Address) rcpt to: [nobody@recipient\_domain](mailto:nobody@recipient_domain)  
       * Use double quotes - mail from: [user@domain](mailto:user@domain) rcpt to: ["user@recipent-domain"](mailto:"user@recipent-domain")  
       * User IP address of the target server - mail from: [user@domain](mailto:user@domain) rcpt to: &lt;nobody@recipient\_domain@\[IP Address\]&gt;  
       * Disparate formatting - mail from: &lt;user@\[IP Address\]&gt; rcpt to: [@domain:nobody@recipient-domain](mailto:@domain:nobody@recipient-domain)  
       * Disparate formatting2 - mail from: &lt;user@\[IP Address\]&gt; rcpt to:   
   * EHLO - Extended SMTP.  
   * STARTTLS - Starts TLS-session to encrypt the traffic.  
   * RCPT - Address of the recipient.  
   * DATA - Starts the transfer of the message contents.  
   * RSET - Used to abort the current email transaction.  
   * MAIL - Specifies the email address of the sender.  
   * QUIT - Closes the connection.  
   * HELP - Asks for the help screen.  
   * AUTH - Used to authenticate the client to the server.  

## Automated Enumeration

* Custom Python script to enumerate supplied usernames \(can be altered to serve from a list\).

  \`\`\`

  **!/usr/bin/python**

  import socket 

  import sys 

  if len\(sys.argv\) !=3: 

  print "Usage: program.py  " 

  sys.exit\(0\) 

## VRFY a user

up\_file = open\(sys.argv\[2\],"r"\) for username in up\_file:

```text
#Create a Socket 
s=socket.socket(socket.AF_INET, socket.SOCK_STREAM) 

#Connect to the Server 
connect=s.connect((sys.argv[1],25))  

#Receive the banner 
banner=s.recv(1024)

s.send('VRFY ' + username) 
result=s.recv(1024) 
if "2.0.0" in result:
    print result

s.close()
```

```text
- Check for availale SMTP commands
```

nmap -script smtp-commands.nse \[IP Address\]

```text
 - Check for any available CVE's or auto-enumeration options through NSE's
```

nmap --script=smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 \[IP\]

```text
- Enumerate common usernames through MSF auxiliary modules
```

msf &gt; use auxiliary/scanner/smtp/smtp\_enum

\`\`\`

