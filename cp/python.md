# PYTHON

### sorting

- in place sorting

```
nums.sort()
```

- using sorted (no inplace sorting)

```
arr2 = sorted(arr1)
```

- key function in boths ways

```python
def keyFunc(x):
    return x[0] + x[1]
arr.sort(key = keyFunc)

# or

sorted(arr, key = lambda x : x[0] + x[1])
```

- use `reverse=True` for reverse
- for string, multiple levels of sorting = concating strings

### Zipping

- can be used for sorting dicts

```py
# sorted according to values
t = sorted(zip(dict.values(), dict.keys()))

# sorted according to keys
t = sorted(zip(dict.keys(), dict.values()))
```

### Asterisk Operator *

- used for deserializing lists into positional args
- used also for deserializing dictionaries into keyword args

```py
print(* list)
foo(** dictionary)
```
- used for functions with variable positional inputs

```py
def addition(* args):
    return sum(args)
```

- used for functions with variable keywords arguments

```py
def foo(**kargs):
    for arg in kargs:
        print(kargs[arg])
```

### heapq

- inserting and deleting element
- do -1 * for max heap

```py
heapq.heapify(heap)
heapq.heappush(heap, n)
n = heapq.heappop(heap)
```

- getting n largest or smallest num

```py
heapq.nlargest(3, arr)
heapq.nsmallest(3, arr)
```

### set

```py
a|b #a union b
a^b #a symmetric difference b, a u b - a n b


17, 19, 42, 25, 38, 89, 54, 98, 89, 67 

58, 29, 24, 67, 52, 89, 45, 98, 79, 13 

```
