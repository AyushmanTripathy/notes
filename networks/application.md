# Application Layer

- on a machine, port is used to identify a process
- interface between application and transport layer are `sockets`
- transport layer is implemented by kernel

### Which transport layer protocol?

1. UDP
    - just end to end packet delivery
    - ex: DNS
1. TCP
    - ordered packet delivery, reliable, connections etc.
    - ex: everything else

## DNS (Domain Name system)

- mapping domain names to IP address
- uses UDP

### Parties

0. Your client
    - has a cache
    - requests resolver for IPs
    - resolvers are preconfigured
1. Recursive Resolver
    - ex: ISP, your organisation etc
    - labels every query with a Query Id
    - every name server, sends the same Query Id with response
    - has a cache
    - recursively queries below three servers.
1. Rootname Server
    - approx 20 of these in the world
    - their IPs are hardcoded
    - provides Toplevel domain Server's IPs
    - ex: NASA
1. Toplevel Domain Servers
    - ex: .com, .org
    - provide Authorative name server IPs
1. Authorative Name server
    - ex: n1.google.com
    - provide the actual IPs

### DNS Record

- also called zone files
- present in Authorative servers, provide info such as IP
- have an associated TTL (time to live) indicating how often to refresh
- types of record
    1. A, IP address
    1. AAAA, IPv6 address
    1. CNAME, forwarding domains or subdomains

### Cache Poisioning

- trying to guess Query Id, before request comes back from name servers
- spamming Query Id and seeing what sticks
- if matched, cache is poisioned with your IP
- TTL can be set high so that cache remains as such

## FTP (File Transfer Protocol)

- connection based, uses TCP
- TFTP is connection less, uses UDP
