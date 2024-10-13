## XOR

-   xor a number twice with a number has no effect
-   its commutative (order is not important)
-   used to findout which number is not duplicate in list

```
a ^ a = 0
a ^ 0 = a
```

## AND

-   counting no of bits (called hamming weight)

```
while n:
    n = n & (n - 1)
    count += 1
```

## OR

-   is setting a 0 bit
