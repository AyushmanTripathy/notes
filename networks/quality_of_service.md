# Quality of Service (QoS)

TCP doesn't prevent congestion, once it occurs it tries to recover from the situation.  
it is considered at network layer because it requies both per hop and end to end behaviour

### Avaliable classes

1. Contant bit rate, telephone
1. Real time variable bit rate, Video conferencing
1. Non real time variable bit rate, Video streaming
1. Avaliable bit rate / Best efforts, File transfer

## Primary Parameters

### Network Bandwidth

Amount of data that can be transmitted in unit time.

### Delay

1. Transmission Delay
    - Time taken to push all packets to the network
1. Propagation Delay
    - Time taken to transfer bit from one end to another
1. Queuing Delay
    - Time taken at interface buffers
    - major component

in general

```
Queuing Delay >> Transmission Delay + Propagation Delay
```

### Jitter

Variation in end to end delay

### Loss

Relative measure of no of packets lost compared to total no of packets.

- its a function of avaliability
- if network is avaliable, loss to be ideally zero.
- not true for wireless networks
