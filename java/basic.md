# Types

## Primitives

1. byte
1. short
1. int
1. long
1. float
1. double
1. char (2 bytes, for unicode)
1. boolean (size is not defined)

-   floats have to be typecasted

```java
float x = (float) 1.0;
float x = 1.0f;
```

### Wrapper Classes

-   primitives have wrapper types, Integer, Float, Boolean etc.
-   all wrapper types are child of `Number` class, except Character.
-   they are interchanged automatically by java

-   `Autoboxing`, primitive converted to wrapper class
-   `Unboxing`, wrapper class converted to primitive

## Generics

-   generic class
-   only reference types are allowed

```java
class Main<T> {}
Main<Integer> m = new Main<Integer>();
```

-   generic function

```java
public <T> void func(T arg) {
    //do something
}
```
