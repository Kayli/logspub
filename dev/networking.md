# notes on a topic of computer networks and related stuff

## basics

- layers of osi model of networking infrastructure
  - 1 physical: electrical signals
  - 2 data: hop to hop delivery using mac addresses
    - arp (address resolution protocol), ethernet
  - 3 network
    - protocols: ipv4/v6, icmp (internet control message protocol), arp, ipsec
  - 4 transport
    - protocols: tcp, udp
  - 5 session
  - 6 presentation: ssl/tls
  - 7 application
    - nearest to the end user, user and application are directly interacting
    - protocols: HTTP/SIP

- bridge network
  - bridge connects two separate networks as if they were a single network
  - is a link layer (level 2) device which forwards traffic between network segments
  - can be a hardware device or a software device running within a host machine’s kernel

- address 0.0.0.0 
  - is a non-routable meta-address used to designate an invalid, unknown or non-applicable target
  - in the context of servers, 0.0.0.0 means all IPv4 addresses on the local machine. 
    - if a host has two IP addresses, 192.168.1.1 and 10.1.2.1, and a server running on the host 
      listens on 0.0.0.0, it will be reachable at both of those IPs


- routing schemes
  - unicast: one to one
  - anycast: one to one of many
  - broadcast: one to many
  - multicast: one to some of many

## http

- http1: uses tcp, requires spearate tcp connection for every request
- http2: uses tcp, introduced http streams, so multiple streams can be used in the same connection
- http3: 
  - uses udp + quic
  - uses connection id to speed-up switching between different networks on mobile devices

- parts: protocol, hostname, path, resource, query string

## check for open ports

- local machine
  - telnet localhost 8080
  - netstat -an | grep :8080

- remote machine
  - when you know specific port
    > telnet remotehost 8080
  - tcp syn scan
    > sudo nmap -sS remotehost
  - tcp connect scan with os detection
    > sudo nmap -sT -O remotehost

- to scan all network devices in your local segment
  - sends only host discovery probes: icmp, tcp syn 443, tcp ack 80, icmp timestamp
  - does not perform scanning of any other ports 
  - command
    > sudo nmap -sn 192.168.1.0/24
  

## load balancing

- level 4 load balancing 
  - offers traffic management of transactions at the network protocol layer (TCP/UDP)
  - delivers traffic with limited network information with a load balancing algorithm 
    (i.e. round-robin) and by calculating the best server based on fewest connections 
    and fastest server response times

- level 7 load balancing 
  - works at the highest level of the OSI model
  - bases its routing decisions on various characteristics of the HTTP/HTTPS header, the 
    content of the message, the URL type, and information in cookies


## ssh

- tunneling
  - by default, anyone (even on different machines) can connect to the specified port on the SSH client machine but this can be restricted to programs on the same host by supplying a bind address:
    > ssh -L 127.0.0.1:80:client.example.com:80 remote.example.com


## tls

- ssl (secure sockets layer) is now considered deprecated, tls is used instead
- uses port 443
- latest version is 1.3
- since tls 1.2 https is faster than http
- tls 1.3 improvements
  - handshake can now be accomplished with a single roundtrip and enables zero roundtrip resumption (0-RTT)

- handshake
  - tls handshake enables the tls client and server to establish the secret keys with which they communicate
  - both symmetric and asymmetric keys are used
  - public key from server is used to encrypt message from client
    - this message contains symmetric key that server should use to form a response

- termination
  - the process of decrypting encrypted traffic before passing it along to a web server


## todo

- subnetting
- gateways
- dhcp/nat


## references

[1]: https://avinetworks.com/glossary/l4-l7-network-services/
[2]: https://www.howtogeek.com/225487/what-is-the-difference-between-127.0.0.1-and-0.0.0.0/