# Switching Networks

- has intermediate switching nodes, for transmission
- two types

## Circuit Switching Networks

- dedicated communication path between stations
- in 3 phases, establish, transfer, disconnect
- for voice traffic
- inefficent incase of channel cpacity wastage
- setup takes some time

## Packet Switching Networks

- stations breaks long messages into packets
- packet is typically 1000 bytes
- can be handled in 2 ways

### Datagram

- can take any route
- can arrive out of order
- can be lost or delayed
- no call setup phase, hence better for few packets
- more flexiable

### Virtual Circuit

- preplanned route before packets are sent
- call request & call accept packets to establish connection (handshake)
- no routing decision for each packet
- packet contain virtual circuit identifier instead of destination address
- less reliable, as all circuits are lost if node is lost.

```
ex: VC Switching Table

| incoming      | outgoing      |
| port  | vci   | port  | vci   |
| 1     | 14    | 3     | 22    |
```

## Devices

### Hubs

- layer 1
- broadcasts to all connected devices
- connects more than 2 devices
- can't filter traffic
- one broadcast & collision domain
- Half Duplex, can't send & receive simultaneously.

### Switch

- layer 2
- muti port bridge
- filters traffic based on MAC address using MAC address tables
- one broadcast domain
- each port is a collision domain
- Full Duplex, can send & receive simultaneously.

### Router

- layer 3
- filters traffic based on IP address
- break up collision & broadcast domains

### NIC

- Network Interface Card acts as the physical layer for computer.
- can be of various types, Wireless, Wired, USB, Fiber Optics
- they have a `MAC` address
- layer 1,2,3 depending on the hardware

## Terms

### Collision Domain

one device's transmission can collide with another due to them sharing a network segment.

### Broadcast Domain

set of devices that hear all broadcasts on a segment

### MAC Address

Media Access control address are unique and assigned by manufacturer.
