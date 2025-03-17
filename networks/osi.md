# Network Protocol Stack

there are layers,

1. Application (HTTP, FTP, SMTP)
1. Transport (TCP, UDP, RTP)
1. Network (IPv4, IPv6, MPLS)
1. Data Link (Ethernet, WiFi, Bluetooth, UMTS, LTE)
1. Physical

also some other protocols, don't fit into single layer.
like DNS, SNMP, ARP, DHCP

## Protocol

- specification for format
- 2 interface
    1. service interface, between application and protocol
    1. peer to peer interface, between two host's protocol
- they are in a hierarchy

### Encapsolution

- data from higher layer becomes payload for lower layer
- high level messages are encapsulated inside low level messages

## OSI Model Layers

Open System Interconnect Model

Higher layer, implemented on end-hosts

1. Application
1. Presentation
    - serializaton, encryption, compression
    - not used anymore
1. Session
    - maintains connections
    - not used anymore
1. Transport
    - TCP layer
    - message or segment
    - adds port, headers

Lower layers, implemented in all network nodes

1. Network
    - packet
    - handles routing for packet switching networks
    - IP Address
1. Data Link
    - frames (aggregates of raw bits)
    - implemented by Network adapter & device drivers
    - MAC address
1. Physical
    - handles transmission over raw bits

## TCP/IP

- is a suite of protocols for inter-networking.
- here layers are organised differently from OSI
- here IP is connectionless and best efforts protocol
- TCP adds reliable and forms a logical connection
- 4, 5 Layers

## Internet Architecture

by IETF  
these layers are not strict, their are an hour glass. IP is the focal point.
