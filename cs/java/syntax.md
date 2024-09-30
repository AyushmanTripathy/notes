# JAVA

The worst programming language

## Keywords

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

### This

- added to variables and methods by compiler, if no name collision
- for refering instance variable with same name

```
this.name = name;
```

- reusing constructors
- call to `this()` must be the first line

```
Student(int x) {}
Student(int x, int y) { this(x); }
```

### Super

- added by compiler, to default constructor
- used to call the parent class constructor
- child class first line must be call to super()

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

## Operators

- relational operators donot work for boolean
- increment operator cannot be chained or applied to constants

### instanceof

```java
obj instanceof cls
```

- gives true if cls is class or super class of obj
- if not gives error
- gives false for null

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

# Mics

- called `extends` because all classes extend from Object already. 
- default value for reference variables is null.
- Java has J capital
