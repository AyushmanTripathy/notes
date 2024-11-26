## Functional Dependency

-   means A determines B

```
A -> B
```

-   required condition is if t1.A = t2.A means t1.B = t2.B
-   here A and B can be set of attributes

### Types

for example, A -> B

1. Trivial
    - if B is a subset of A
1. Semi Non Trivial
    - if B is not a subset of A
1. Non Trivial
    - if A intersect B is null
1. Multi valued
    - A -> BC
    - no functional dependency between B and C
1. Transitive
    - A -> B and B -> C implies A -> C
1. Partial
    - if any proper subset of candidate key 
    - defines a non prime attribute
1. Fully
    - not a partial FD

### Armstrong's Axioms

properties of funcational dependencies.  
primary rules are,

1. Reflexivity, A -> A
1. Transitivity, A -> B and B -> C implies A -> C
1. Augmentation, A -> B implies AC -> BC

secoundary rules,

1. Union, A -> B and A -> C implies A -> BC
1. Composition, A -> B and C -> D implies AC -> BD
1. Decomposition, A -> BC implies A -> B and A -> C
1. Pseudo Transitivity, A -> B and BC -> D implies AC -> D

### Attribute Closure

-   set of all atributes derived from an attribute
-   denoted by `A+`

### Prime Attributes

-   attributes which are part of a candidate key

### Equivalence

-   for 2 sets of FDs, fd1 and fd2
-   fd1 ⊃ fd2 if all fds in fd2 can be derived from fd1
-   fd2 ⊃ fd1 if all fds in fd1 can be derived from fd2
-   if both are true, we say fd1 = fd2

### Extraneous Attributes

-   if a attribute infered, is already infered
-   B is extraneous in both cases

```
AB -> C, A -> C
AB -> C, A -> B
```

### Canonical Cover

minimal set of FDs equivalent to given FD set.  
steps to find cover,

1. split all FDs
1. check for repeated attributes
