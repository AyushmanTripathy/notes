# PYTHON

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

- getting n largest or smallest num

```py
heapq.nlargest(3, arr)
heapq.nsmallest(3, arr)
```
