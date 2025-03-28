# Transport Layer

- ensures end to end communication
- implemented by the kernel

### Services Provided

- Network layer provides only Datagram delivery (unreliable)
- unlike TCP, UDP doesnot provide below services

1. Connection Establistment
1. Reliable Data Delivery
    - network layer can drop packets
    - ensuring delivery, even if packets are dropped
1. Flow control
    - agreed upon rate of delivery (flow control)
    - faster device doesn't overwhelm slower device
1. Congestion control
    - avoids congestion on junctions
1. Ordered Packet delivery

## Connection Establistment

### Delayed Duplicated Delivery

- to ensure reliability, packets are resend after a timeout
- differentiating between such packets is different
- machine can also crash after initiating connection request

### Solutions

1. using throwaway port numbers (transport address)
    - changing port number after program crashes
    - port number are limited
1. assigning unique identifier choosen by client
    - how to ensure its unique globally
1. each packet has a lifetime
    - we kill of aged packets
    - putting a hop count in each packet
    - timestamping in each packet, requires time synchronization (hard)

### Acknowledgement Problem

- when a packet dies, we need to ensure, all acknowledgements of it are also dead
- problem it prevents
    - client sends req 1
    - client restarts due to crash
    - client sends req 2
    - client receives res 1
    - how will client know res 1 is for req 1 or req 2

### Solution

Maximum packet lifetime, `T`

- time after packet is send when its completely dead
- packet and its anknowledgments

Choosing a Sequence Number

- label segment with a sequence number
- that no is not resued for T.
- ensures that at any time there is only one packet with unique no.
- size is determined by T and rate of packets per secound.

Properties of Sequence Number

- a seq no does not refer to more than one byte
- valid range of sequence numbers must be synchronized

```
| seq no | len | payload |
if len is 100, payload length has 100 bytes
seq no is ex: 500, means 500 - 600 bytes are present here
```

### deciding initial sequence no

- goal is to make seq no unqiue for each byte in a network, at any time
- problem of crashing

![problem of client crashing](../media/21d1cf8a.jpg)

- 2 solutions
- wait for packets to die off completely
- if the new connection sends too much data too fast
- it can forbidden range can still overlap
- same problem if data is send too slow in previous connection

![waiting for packets to die](../media/a448ef5c.jpg)

- choose a different higher seq no

![choosing a higher seq no](../media/f90c0746.jpg)

- here the range between two connections is `forbidden range`

### Self Clocking

- `clock tick` inter packet transmission duration
- only one segment per clock tick
- data is transmissted at bounded rate to prevent seq no wrap around

### Three Way Handshake

- ensure that receiver doesnot need to remember seq no.
- provides `positive syncronisation`
- ACK denotes, what seq no a host is expecting
- if received SYN and ACK is invalid we know its a delayed duplicate

steps

- host 1 sends SYN x
- host 2 reply with an ACK x, and SYN y
- host 1 then sends ACK y with SYN x

## Connection Release

### Asymmetric Release

- if one pary releases connection, its broken
- this can lead to data loss

Two army problem

- two army in the hills needs to attack simultaneously
- but another army is in the valley
- no protocol exists for this case

### Symmetric Release

- treats connections as two unidirectional connections
- both need to release separetly
- good when, each process know how data it needs to be know

steps

- host 1 initiates
    - sends FIN
    - waits for ACK
- host 2 will recieve FIN
    - send a ACK
    - starts releasing connection
    - sends FIN after that
- host 1 after recieving ACK
    - waits for FIN
- host 1 recives FIN
    - release connection
    - connection is closed

incase packets fail,

- host 1 will send FIN for N times with timeouts in between
- if all timeouts fail, it will release
- host 2 once its receives a FIN, will set timeout
- if timeout fails, it will release

## Flow Control & Reliablity

- ensures the data transmission is not more that what receiver can receive.
- at both data link and transport layer
- if implemented only at data link layer, buffers at router will overflow.
- if implemented only at transport layer, incoming rate is more than outgoing rate in a router.

### Stop and wait (Automatic Repeat Request)

- after sending one frame, we wait for ACK
- after timeouts we resend the frame
- we only need seq no 0 and 1
- for directional, we need two instances

### Sliding Window Protocol

- parrallely sending and receiving, packets and ACKs.
- sending N (window size) without waiting for ACK
- after receiving ACK we reduce the window.
- `Outstanding Frames` are frames that are transmitted but not ACK'd
- MAX SEQ is 2 ^ n, for n bit seq no

TYPES

1. go back n arq, if a frame is lost, all frames are retransmitted
    - window size is MAX SEQ - 1
1. selective repeat arq, only lost frames are retransmitted
    - NAK (SACK), receiver sends which frames are lost
    - if all frames received, one (cumulative) ACK with next seq no
    - if a frame is not received, NAK with the seq no
    - window size if (MAX SEQ + 1) / 2


## Performance 

### Bandwidth Delay Product

```
BDP = link bandwith * link delay 
```

- no of segments needed in channel, bandwith delay * 2
- now no of bits for seq no can be calculated
- for maximum utilisation, window sizee = 2 * BD + 1
- ex: if BDP is less than segment size, stop and wait is used

Round trip time

- total time to send data & receive acknowledgement
- twice the one way latency

### Transport Buffer Pool

can be

1. Variable Size buffers
    - better memory utilisation
    - complicated implementation
    - for each segments in a linked list
1. Circular size buffer
    - for each connection
    - easier implementation

## Buffer Managment

required because 

- because reading rate & receiving rate can be different.
- receiver needs a dynamic buffer to store data temporarily.
- sender should not send more data compared to buffer size.

solution

- continious ACKs with buffer size
- sender waits for buffer size to be free before sending

## Congestion Control

problem

- decentralised network, hence no algoritihm can be applied
- cannot apply max flow min cut theorem
- bandwith also changes after connections are added/removed.

hence we can only do congestion avoidance

### Congestion Avoidance

regulating sending rate

```
Sending rate = min(network rate, receiving rate)
```

working

- receiving rate: advertised by receiver during sliding window flow control
- gradually increase network rate
- observing the packet loss

### Fairness

problem

- bad congestion control can affect fairness
- i.e. some connections can strave
- Hard fairness is difficult to implement

Max Min Fairness

- bandwidth is conserved
- bandwidth cannot be increased for a connection without decreasing bandwith for another conneciton

#### Additive Increase Multiplicative Decrease

algorithim to provide max min fairness

```
w(t + 1) = w(t) + a     if no congestion
         = w(t) * b     if congestion
```

where a > 0 and 0 < b < 1  
advantage

- other AIAD and MIMD occilate around
- this algorithim converges towards optimal point

