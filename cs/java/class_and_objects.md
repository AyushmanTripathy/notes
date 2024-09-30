# Class & Objects

## Class

-   blueprint of an object
-   its only a logical entity

```java
class ClassName {
    //feilds
    //methods
}
```

-   `Instance variables` declared in class, outside methods
-   they get memory when object is created.

### Constructors

-   block of code, called when object is created
-   default no arg constructor for every class

rules for constructors,

1. no explicit prototype (return type)
1. name is same as class name
1. can have access modifiers
1. cannot use abstract, static, final, synchronized

types of constructors,

1. no arg or non parameterised
1. parameterised

-   Constructors can be overloaded based on no of args and their types
-   return value is the object created.

### Initializer Blocks

-   runs before the constructor
-   used for code common to all constructors

```java
class Class {
    int x;
    {
        x = 10;
    }
}
```

## Objects

-   instance of class
-   logical and physical entity
-   it has `state` and `behaviour`
-   can have their own propertise
-   stored in heap memory and used by reference variables.
-   reference variables are stored in stack memory.

```
Class obj = new Class();
```

- `public String toString()` is used to print a object
- references can be identified by hash code.

```java
System.identityHashCode(ref);
Object.hashCode(ref); //calls the above
```
