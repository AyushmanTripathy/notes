# [codechef START121C](https://www.codechef.com/START121C)

## Anti Adjacent Swaps

### Problem

Array has to sorted, adjacent pairs cannot be swapped
if possible "yes" else "no"

### Solution

if len(arr) >= 4 then always possible
else cases

# [codechef START127D](https://www.codechef.com/START127D)

## Superincreasing

### Problem

superincreasing means A[i] > A[i - 1] + ... + A[0]
can you form a array where Kth index has X

### Solution

minimum sum array is [1, 2, 4, ... , 2 ^ i]
if X > 2 ^ (i - 1) then yes else no
