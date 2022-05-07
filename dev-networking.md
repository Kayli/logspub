# notes on a topic of computer networks and related stuff

## basics

- layers of osi model of networking infrastructure
  - L1 physical: electrical signals
  - L2 data
    - examples: ARP (address resolution protocol), ethernet
  - L3 network
  - L4 transport
    - transmission of data between points on a network
    - example protocols: TCP/UDP
  - L5 session: manages connections between apps
  - L6 presentation: ssl/tls
  - L7 application
    - nearest to the end user, user and application are directly interacting
    - example protocols: HTTP/SIP


## load balancing

- L4 load balancing 
  - offers traffic management of transactions at the network protocol layer (TCP/UDP)
  - delivers traffic with limited network information with a load balancing algorithm 
    (i.e. round-robin) and by calculating the best server based on fewest connections 
    and fastest server response times

- L7 load balancing 
  - works at the highest level of the OSI model
  - bases its routing decisions on various characteristics of the HTTP/HTTPS header, the 
    content of the message, the URL type, and information in cookies


## references

[^1]: https://avinetworks.com/glossary/l4-l7-network-services/
