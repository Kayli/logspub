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


## tcp/ip

- tcp/ip reference model does not concern itself with the OSI model's details of application or transport protocol semantics and therefore does not consider a session layer

- three-way handshake
  - sequence of packets to establish connection between two parties
  - sequence number
    - initially isn (initial sequence number) is a randomly generated one
    - gets incremented 
      - either by one
      - or for the amount of data (payload) being sent in acknowledgment number
  - acknowledgment number
    - incremented sequence number
  - packets: syn, syn-ack, ack

- mtu: maximum transmission unit
  - data including headers for tcp 20 bytes and ip 20 bytes
  - packets bigger than the mtu are fragmented at the point where the lower MTU is found and reassembled further down the chain

- mss: maximum segment size
  - maximum size of the application data chunk in this message, not counting the TCP headers
  - derived from the mtu
  - packets exceeding mss aren't fragmented, they're simply discarded

- window size: the amount of data "in flight", ie. being transmitted before an ack is required


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


## references

[^1]: https://avinetworks.com/glossary/l4-l7-network-services/
