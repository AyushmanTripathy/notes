# PYTHON

### floor division

- is not integral division like in c

```py
-1 // 10        # -1
int(-1 / 10)    # 0 (correct)
```

### comparison operator

- method like `__eq__`, `__lt__` can be defined for comparisons
- all can be defined automatically by using `total_ordering`

```python
from functools import total_ordering

@total_ordering
class Example:
    def __lt__(self, other):
        return self < other
```

- if comparison is defined for `__eq__`, use is None to check

### sorting

- in place sorting

```py
nums.sort()
```

- using sorted (no inplace sorting)

```
arr2 = sorted(arr1)
```

- when sorting list of tuple, index denotes priority
- 1st index will have most priority

- key function in boths ways
- can also return tuples

```python
def keyFunc(x):
    return x[0] + x[1]
arr.sort(key = keyFunc)
# or
sorted(arr, key = lambda x : x[0] + x[1])
```

- use `reverse=True` for reverse
- for string, multiple levels of sorting = concating strings

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

- x is no of chars (including '.')
- y is no of decimal places
- left padded with spaces

```
f"{a:x.yf}"
```

- possible for ints also
- if len(int) > x, then complete int is printed

```
f"{a:xd}"
```

- similar for strings
- **Exception** unlike c, strings are right padded

```
f"{a:xs}"
```

### Zipping

- used to combine to two list or strings
- returns a object, which does not support `[]`

```py
zip([1, 2, 3], [4, 5]) # -> (1, 4), (2, 5)
```

- len(output) = min(len(a), len(b))

- can be used for sorting dicts

```py
# sorted according to values
t = sorted(zip(dict.values(), dict.keys()))

# sorted according to keys
t = sorted(zip(dict.keys(), dict.values()))
```

### Enumerate

- used to combine element with there index
- returns a object, which does not support `[]`

```py
enumerate([3, 2, 1]) # -> (0, 3), (1, 2), (2, 1)
```

- can be combined with zip

### Asterisk Operator \*

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

### Colon Equal `:=`

- used to set a variable within a expression
- evaluates to value that was set

```
print(n := 10) #10
n := 10        #gives an error
(n := 10)      #valid
```

### heapq

- inserting and deleting element
- do -1 \* for max heap

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
```

### time

```py
import time
time.sleep(1)
print(time.time())
```

### Threading

```py
# without class
t = Thread(target=func, args=('arg for func'))

# extend class
class MyThread(thread):
    def run(self):
        print("something")
t = MyThread()

# dont extend class
t = Thread(target=t.run)

t.start()
```

| Property/Method            | Description                            |
| -------------------------- | -------------------------------------- |
| threading.current_thread() | obj of thread                          |
| start()                    | start the thread                       |
| ident                      | identification number                  |
| getName()                  | name of thread                         |
| setName()                  | name of thread                         |
| active_count()             | no of threads                          |
| enumerate()                | loop over active threads               |
| isAlive()                  | check if active                        |
| join(n?)                   | optionally wait for thread upto n secs |
| setDaemon(), isDeamon()    | deamon threads                         |

on threads,

- daemon status is inherited from parent thread
- all daemon threads terminate after last non daemon thread

### Synchronization

Locks

- `aquire()` and `release()`
- blocks if same thread aquires twice

RLocks (Rentrant Lock)

- lock can be reaquired by same thread
- no of calls of aquire and release should match

Semaphore

- locks but for n process
- no bound for no of release calls
- hence `BoundedSemaphore` is used

### Inter Process Comunication

Event

```py
from threading import Event

def consumer():
    event.wait()
def producer():
    event.set()
    event.clear()

event=Event()
```

### Mics

- `inf` type is float
- leading zeros are not permitted, but `00` is fine.

```py
x = 01 #SyntaxError
```

- maximum length of identifier is 31
- future typing by

```py
from __future__ import annotations
```
