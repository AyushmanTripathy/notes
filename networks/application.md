# Application Layer

- on a machine, port is used to identify a process
- interface between application and transport layer are `sockets`
- transport layer is implemented by kernel

### Which transport layer protocol?

1. UDP
    - just end to end packet delivery
    - ex: DNS, SNMP
1. TCP
    - ordered packet delivery, reliable, connections etc.
    - ex: DNS, everything else

## DNS (Domain Name system)

- mapping domain names to IP address
- inverse mapping is also avaliable
- each domain name served by 2 DNS servers
- uses TCP or UDP

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

## Client Server Paradigm

- client & server are different process
- server is always listening for requests
- two types
    1. iterative, single server process handles all requests
    1. concurrent, child server process for each requests

## FTP (File Transfer Protocol)

- connection based, uses TCP
- TFTP is connection less, uses UDP, uses 69
- makes two connections
    1. control connection, port 21
    1. data connection, port 20, unidirectional

## HTTP (Hypertext Tranfer Protocol)

- transport protocol independent
- supports mutiple request/reply over single connection
- default port is 80
- components
    - URL (protocol://host:port/path)
    - Cookie
- document types
    - static page 
    - dynamic page  (server site scripting)
    - active page   (client site scripting)

### HTTP Proxy Server

```
client <-> proxy <-> server
```
## SMTP (Simple Mail Transfer Protocol)

- port 25

### MIME (Multipurpose internet mail extension)

- allows support for non ASCII (images, audio, etc)
- has headers, like http

### Mail Accress Protocol

- retrives email from user's mailbox
- types
    1. POP3 (Post Office Protocol)
        - allows users to get a list of emails
        - retrieve their email
        - delete/keep emails
    1. IMAP4 (Internet Mail Access Protocol v4)
        - has more features
        - headers can be checked before downloading
        - users can download parts of emails

## SNMP (Simple Network Managment Protocol)

- montior and manage networks
- SNMP manager and some SNMP agent
- uses UDP
