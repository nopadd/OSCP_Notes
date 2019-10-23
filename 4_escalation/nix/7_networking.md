# 7\_Networking

## What NIC's Exist & Connection Status To Other Networks

```text
/sbin/ifconfig -a 
cat /etc/network/interfaces 
cat /etc/sysconfig/network
```

## Network Configurations \(DHCP, DNS, Gateway Servers\)

```text
cat /etc/resolv.conf 
cat /etc/sysconfig/network 
cat /etc/networks 
iptables -L 
hostname 
Dnsdomainname
```

## Other Hosts / Users Communicating w/ Host

```text
lsof -i 
lsof -i :80 
grep 80 /etc/services 
netstat -antup 
netstat -antpx 
netstat -tulpn 
chkconfig --list 
chkconfig --list | grep 3:on 
last 
W
```

## Cached IP / MAC Address

```text
arp -e 
route 
/sbin/route -nee
```

## Listen To Live Traffic

```text
tcpdump tcp dst [ip] [port] and tcp dst [ip] [port]
```

