# Path Finding

- Weighted Graph has Vertices(V), Edges(E), each edges has Weight(w)
- Maximum number of edges is V^2
- algorithims are independent of range of weights

### General Structure

- for non negative weights
- `relaxation` means updaing vertices

```
initiate for all V
distance(v) <- inf and predecessor(v) <- null
distance(start_node) <- 0

repeat
    select edge (x, y)
    if distance(y) > distance(x) + weight(x,y)
        update distance(y)
        predecessor(y) = x
    until no more relaxation
```

- how to choose next node -> depends on algorithim
- simple one is like Breath First Search.

### Dikstra's Algorithim

```
Q -> priority queaue with unknown shortest path
S -> set of Vertices with known shortest path

while Q is not empty
    // delete min from Q
    u <- extract_min(Q)      
    // add min in S
    S = S U { u }            
    for each v adjacent to u   
        relax(u, v, weight)
```
