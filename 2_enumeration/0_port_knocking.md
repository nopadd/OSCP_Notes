# 0\_Port\_Knocking

## Background

Sometimes there are services and ports open on the local host that we can't see or identify with the traditional nmap searching / scanning. This is when we have to do port knocking to open up these hidden ports / services.

1. You can see this if you are on the local host.

   ```text
   netstat –alnp | grep LIST
   ```

## Attack Vector \(ippsec:Nineveh\) \(Vulnhub:Lord of the Root\)

The Knockd service establishes what port knocking sequence is necessary to "unlock" a hidden port to the outside. 1. You can identify if the knockd service is being used by the host by:

```text
Cd init.d; ls
```

1. See if knockd is in the list.
2. If it is in the list, the knock sequence is found in Knockd's default file for system configuration \(generally in /etc/default/knockd\).
3. If the ports listed in the sequence variable are knocked \(sent a TCP packet\) in the correct order, then a certain command is executed to open up a port.

   ```text
   for I in [port knock sequence like:1 2 3]; do nmap -Pn -p $I --max-retries 0 [IP address]; done 
   knock [IP address] [port knock squence like:1 2 3]
   ```

   * Knock is a small binary that is downloaded as part of the knockd package from apt.

4. Then you can nmap for the port to see it's open / unfiltered. 

