# JAVA

The worst programming language

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

- floats have to be typecasted

```java
float x = (float) 1.0;
float x = 1.0f;
```

- all have wrapper types, Integer, Float, Boolean etc.
- all wrapper types are child of `Number` class, except Character.

### Break Label

- used to break out of outer loops

```java
label:
while (true) {
    while (true) {
        break label;
    }
}
```

### Final

- final methods prevents overriding (methods on Objects)
- final classs prevents inheritane (Wrapper classes)

#### final variables 

- can be initialized once
- naming convention is upper snake case
- legal examples

```java
final double PI;
PI = 3.14;

for (final int i : arr);
```

## Arrays

- are themselves Objects

```java
int[] arr;              //declaring arr
arr = new int[size];    //initializing arr
int[] arr = { 1, 2, 3, 4, 5 };
```

rules for declaring arrays

1. dimension coming before 1st object applies to all.
1. only 1st object can have dimension before it.
1. dimension coming after object applies to only themselves.

```
int[] []a[], b[], c[]; //Valid;
```

- `[` means 1 dimension, `I` means int type and then a hexcode.

```java
System.out.println(arr) //[I@17211155
```

- array's size can be 0 but not negative

### Jagged Arays

- mutidimensional arrays with different sizes

```java
int a[][] = new int[2][];
a[0] = new int[3];
a[1] = new int[2];

// OR
int a[][] = { new int[2], new int[4] };
```

## String

- java has no operator overloading
- exception is `+` for strings

# Operators

- relational operators donot work for boolean
- increment operator cannot be chained or applied to constants

### instanceof

```java
obj instanceof cls
```

- gives true if cls is class or super class of obj
- if not gives error
- gives false for null

# Class & Objects

## Class

- blueprint of an object
- its only a logical entity

```java
class ClassName {
    //feilds
    //methods
}
```

- `Instance variables` declared in class, outside methods
- they get memory when object is created.

### Constructors

- block of code, called when object is created
- default no arg constructor for every class

rules for constructors,

1. no explicit prototype (return type)
1. name is same as class name
1. can have access modifiers
1. cannot use abstract, static, final, synchronized

types of constructors,

1. no arg or non parameterised
1. parameterised

- Constructors can be overloaded based on no of args and their types
- return value is the object created.

### Initializer Blocks

- runs before the constructor
- used for code common to all constructors

```java
class Class {
    int x;
    {
        x = 10;
    }
}
```

## Objects

- instance of class
- logical and physical entity
- it has `state` and `behaviour`
- can have their own propertise
- stored in heap memory and used by `reference` variables.
- reference variables are stored in stack memory.

## Variables

### Local variables

- defined inside method block
- cannot be static

### Instance variables

- defined inside class block outside method block
- specific to each instance

### Static variables

- defined inside class block outside method block
- shared across all instances of class

### Anonymous Objects

- have no reference variables

```java
new ClassName().method();
```

## Polymorphism

2 types in Java

### Overloading

- for method or constructor
- same class, different function signatures
- no, type and order of arguments
- return type doesn't count

### Overriding

- for only method
- same function signatures, different class

# Mics

- called `extends` because all classes extend from Object already. 
- default value for reference variables is null.
- Java has J capital
