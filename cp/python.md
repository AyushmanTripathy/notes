# PYTHON

### floor division

- is not integral division like in c

```py
-1 // 10        # -1
int(-1 / 10)    # 0 (correct)
```

### sorting

-   in place sorting

```
nums.sort()
```

-   using sorted (no inplace sorting)

```
arr2 = sorted(arr1)
```

-   when sorting list of tuple, index denotes priority
-   1st index will have most priority

-   key function in boths ways
-   can also return tuples

```python
def keyFunc(x):
    return x[0] + x[1]
arr.sort(key = keyFunc)

# or

sorted(arr, key = lambda x : x[0] + x[1])
```

-   use `reverse=True` for reverse
-   for string, multiple levels of sorting = concating strings

### String formating

1. F string

```py
f"My name is {x}"
```

1. format()

```py
"My name is {}".format(x)
```

1. % Operator

```py
"My name is %s" %x
"My name is %s and is %s" %(x, y)
```

### Number formating

-   x is no of chars (including '.')
-   y is no of decimal places
-   left padded with spaces

```
f"{a:x.yf}"
```

-   possible for ints also
-   if len(int) > x, then complete int is printed

```
f"{a:xd}"
```

-   similar for strings
-   **Exception** unlike c, strings are right padded

```
f"{a:xs}"
```

### Zipping

-   used to combine to two list or strings
-   returns a object, which does not support `[]`

```py
zip([1, 2, 3], [4, 5]) # -> (1, 4), (2, 5)
```

-   len(output) = min(len(a), len(b))

-   can be used for sorting dicts

```py
# sorted according to values
t = sorted(zip(dict.values(), dict.keys()))

# sorted according to keys
t = sorted(zip(dict.keys(), dict.values()))
```

### Enumerate

-   used to combine element with there index
-   returns a object, which does not support `[]`

```py
enumerate([3, 2, 1]) # -> (0, 3), (1, 2), (2, 1)
```

-   can be combined with zip

### Asterisk Operator \*

-   used for deserializing lists into positional args
-   used also for deserializing dictionaries into keyword args

```py
print(* list)
foo(** dictionary)
```

-   used for functions with variable positional inputs

```py
def addition(* args):
    return sum(args)
```

-   used for functions with variable keywords arguments

```py
def foo(**kargs):
    for arg in kargs:
        print(kargs[arg])
```

### Colon Equal `:=`

- used to set a variable within a expression
- evaluates to value that was set

```
print(n := 10) #10
n := 10        #gives an error
(n := 10)      #valid
```

### heapq

-   inserting and deleting element
-   do -1 \* for max heap

```py
heapq.heapify(heap)
heapq.heappush(heap, n)
n = heapq.heappop(heap)
```

-   getting n largest or smallest num

```py
heapq.nlargest(3, arr)
heapq.nsmallest(3, arr)
```

### set

```py
a|b #a union b
a^b #a symmetric difference b, a u b - a n b
```

### Mics

- `inf` type is float
- leading zeros are not permitted, but `00` is fine.

```py
x = 01 #SyntaxError
```

- maximum length of identifier is 31
- 
