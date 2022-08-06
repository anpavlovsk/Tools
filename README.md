# Tools
Debugging and networking troubleshooting tools
### Commands


### host
Host command is for the reverse lookup of IP or a DNS name.

For example, If you want to find a DNS attached with an IP you can use the host commands as follows.
````
host 8.8.8.8
````
You can also do the reverse to find the IP address associated with the domain name. For example,
````
host google.com
````
### ping
The ping networking utility is used to check if the remote server is reachable or not. It is primarily used for checking the connectivity and troubleshooting the network.

It provides the following details.
Bytes sent and received 
Packets sent, received, and lost 
Approximate round-trip time (in milliseconds) 
Ping command has the following syntax. 

ping <IP or DNS>
For example,
````
ping google.com
````
To ping IP address
````
ping 8.8.8.8
````
If you want to limit the ping output without using ctrl+c, then you can use the “-c” flag with a number as shown below.
````
ping -c 3 google.com
````
### curl
Curl utility is primarily used to transfer data from or to a server. However, you can use it for network troubleshooting.

For network troubleshooting, curl supports protocols such as DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, MQTT, POP3, POP3S, RTMP, RTMPS, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET and TFTP

For example, curl can check connectivity on port 22 using telnet.
````
curl -v telnet://192.168.33.10:22
````
You can check the FTP connectivity using curl.
````
curl ftp://ftptest.net
````
You can troubleshoot web server connectivity as well.
````
curl http://google.com -I
````
nc (netcat)
The nc (netcat) command is known as the swiss army of networking commands.

Using nc, you can check the connectivity of a service running on a specific port.

For example, to check if ssh port is open, you can use the following command.

nc -v -n 192.168.33.10 22
netcat can also be used for data transfer over TCP/UDP and port scanning.

Port scanning is not recommended in cloud environments. You need to request the cloud provider to perform port scanning operations in your environment.

telnet
The telnet command is used to troubleshoot the TCP connections on a port.

To check port connectivity using telnet, use the following command.

telnet 10.4.5.5 22

route
The “route” command is used to get the details of the route table for your system and to manipulate it. Let us look at a few examples for the route command.

Listing all routes
Execute the “route” command without any arguments to list all the existing routes in your system or server.

ubuntu@devopscube:~$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         ip-172-31-16-1. 0.0.0.0         UG    0      0        0 eth0
172.17.0.0      *               255.255.0.0     U     0      0        0 docker0
172.31.16.0     *               255.255.240.0   U     0      0        0 eth0
ubuntu@devopscube:~$
If you want to get the full output in numerical form without any hostname, you can use “-n” flag with the route  command.

ubuntu@devopscube:~$ route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         172.31.16.1     0.0.0.0         UG    0      0        0 eth0
172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 docker0
172.31.16.0     0.0.0.0         255.255.240.0   U     0      0        0 eth0
ubuntu@devopscube:~$


wget
The wget command is primarily used to fetch web pages.

You can use wget to troubleshoot network issues as well.

For example, you can troubleshoot proxy server connections using wget.

wget -e use_proxy=yes http_proxy=<proxy_host:port> http://externalsite.com
You can check if a website is up by fetching the files.

wget www.google.com

ip (ifconfig)
ip command is used to display and manipulate routes and network interfaces. ip command is the newer version of ifconfig. ifconfig works in all the systems, but it is better to use ip command instead of ifconfig.

Let’s have a look at a few examples of ip command.

Display network devices and configuration
ip addr
You can use this command with pipes and grep to get more granular output like the IP address of the eth0 interface. It is very useful when you work on automation tools that require IP to be fetched dynamically.

The following command gets the IP address of eth0 network interface.

ip a | grep eth0  | grep "inet" | awk -F" " '{print $2}'
Get details of a specific interface

ip a show eth0
You can list the routing tables.

ip route
ip route list

arp
ARP (Address Resolution Protocol) shows the cache table of local networks’ IP addresses and MAC addresses that the system interacted with.

arp
Example output,

vagrant@dcubelab:~$ arp
Address                  HWtype  HWaddress           Flags Mask            Iface
10.0.2.3                 ether   52:54:00:12:35:03   C                     eth0
192.168.33.1             ether   0a:00:27:00:00:00   C                     eth1
10.0.2.2                 ether   52:54:00:12:35:02   C                     eth0

arp
ARP (Address Resolution Protocol) shows the cache table of local networks’ IP addresses and MAC addresses that the system interacted with.

arp
Example output,

vagrant@dcubelab:~$ arp
Address                  HWtype  HWaddress           Flags Mask            Iface
10.0.2.3                 ether   52:54:00:12:35:03   C                     eth0
192.168.33.1             ether   0a:00:27:00:00:00   C                     eth1
10.0.2.2                 ether   52:54:00:12:35:02   C                     eth0

ss (netstat)
The ss command is a replacement for netstat. You can still use the netstat command on all systems.

Using ss command, you can get more information than netstat command. ss command is fast because it gets all the information from the kernel userspace.

Now let’s have a look at a few usages of ss command.

Listing all connections
The “ss” command will list all the TCP, UDP, and Unix socket connections on your machine.

ubuntu@devopscube:~$ ss
Netid  State      Recv-Q Send-Q   Local Address:Port       Peer Address:Port
u_str  ESTAB      0      0                    * 7594                  * 0
u_str  ESTAB      0      0      @/com/ubuntu/upstart 7605                  * 0  
u_str  ESTAB      0      0                    * 29701                 * 0
u_str  ESTAB      0      0      /var/run/dbus/system_bus_socket 29702                 * 0
tcp    ESTAB      0      400      172.31.18.184:ssh         1.22.167.31:61808
The output of the ss command will be big so you can use ” ss | less ” command to make the output scrollable.

Filtering out TCP, UDP and Unix sockets
If you want to filter out TCP , UDP or UNIX socket details, use “-t” “-u” and “-x” flag with the “ss” command. It will show all the established connections to the specific ports. If you want to list both connected and listening ports using “a” with the specific flag as shown below.

ss -ta
ss -ua
ss -xa
List all listening ports
To list all the listening ports, use “-l” flag with ss command. To list specific TCP, UDP or UNIX socket, use “-t”, “-u” and “-x” flag with “-l” as shown below.

ubuntu@devopscube:~$ ss -lt
State      Recv-Q Send-Q      Local Address:Port          Peer Address:Port
LISTEN     0      128                     *:ssh                      *:*
LISTEN     0      50                     :::http-alt                 :::*
LISTEN     0      50                     :::55857                   :::*
LISTEN     0      128                    :::ssh                     :::*
LISTEN     0      50                     :::53285                   :::*
ubuntu@devopscube:~$
List all established
To list all the established ports, use the state established flag as shown below.

ss -t -r state established
To list all sockets in listening state,

ss -t -r state listening

traceroute
If you do not have a traceroute utility in your system or server, you can install it from the native repository.

traceroute is a network troubleshooting utility. Using traceroute you can find the number of hops required for a particular packet to reach the destination.

For example,

traceroute google.com

mtr
The mtr utility is a network diagnostic tool to troubleshoot the network bottlenecks. It combines the functionality of both ping and traceroute

For example, the following command shows the traceroute output in real-time.

mtr google.com

mtr report
You can generate a report using the –report flag. When you run the mtr report, it sends 10 packets to the destination and creates the report.

mtr -n --report google.com

dig
If you have any task related to DNS lookup, you can use “dig” command to query the DNS name servers.

Get all DNS records with dig
The following command returns all the DNS records and TTL information of a twitter.com

dig twiter.com ANY
all DNS records with dig
Use +short to get the output without verbose.

dig google.com ANY +short
Get Specific DNS Record with dig
For example, If you want to get the A record for the particular domain name, you can use the dig command. +short will provide the information without verbose

dig www.google.com A +short
Similarly, you can get the other record information separately using the following commands.

dig google.com CNAME +short
dig google.com MX +short
dig google.com TXT +short
dig google.com NS +short
Reverse DNS Lookup with dig
You can perform a reverse DNS lookup with dig using the following command. Replace 8.8.8.8 with the required IP

dig -x 8.8.8.8

nslookup
Nslookup (Name Server Lookup) utility is used to check the DNS entries. It is similar to dig command.

To check the DNS records of a domain, you can use the following command.

nslookup google.com
You can also do a reverse lookup with the IP address.

nslookup 8.8.8.8
To get all the DNS records of a domain name, you can use the following.

nslookup -type=any google.com
Similarly, you can query for records like mx, soa etc

some usefull linux commands
https://www.youtube.com/watch?v=AVXYq8aL47Q&ab_channel=Linode

https://github.com/kodekloudhub/linux-basics-course/blob/master/docs/07-Networking/04-Troubleshooting.md

https://devopscube.com/list-linux-networking-troubleshooting-and-commands-beginners/
