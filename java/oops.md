# Pillars of OOPs

## Abstraction

- hides implementation details
- using abstract classes and interface

```java
// Car is a abstract class
// Honda is a child class of car
Car c = new Honda();
c.stop();
```

## Encapsulation

- bundling code and data together
- private variables, getters & setters

## Polymorphism

2 types in Java

### Overloading

-   for method or constructor
-   same class, different function signatures
-   no, type and order of arguments
-   return type doesn't count

```java
class B {}
class C extends B {}

class A {
  static void m(B a) {
    System.out.println("super");
  }
  static void m(C a) {
    System.out.println("sub");
  }
}

B b = new B();
C c = new C();
B d = c;
A.m(b);     //super
A.m(c);     //sub
A.m(c);     //super without m(C a)
A.m(d);     //super
```

-   depends on the type of reference, not the object
-   if not avaible, try to convert the parent reference

### Overriding

-   for only method
-   same function signatures, different class

## Inheritance

```java
class A {
  int x = 10;
  static void print() {
    System.out.println("A");
  }
}

class B extends A {
  int x = 20;
  static void print() {
    System.out.println("B");
  }
}

class Main {
  public static void main(String args[]) {
    A obj = new B();
    obj.print()                 //A
    System.out.println(obj.x)   //10
    obj.print();
  }
}
```


### Interface

-   until java v1.7, non abstract methods are not supported.
-   every variable is public static final
-   every function is by default public abstract
-   to prevent use `default` keyword

```java
interface Name {
    int x;
    void m();
    default void n() {
    }
    static void o() {
        //public static non abstract
        //abstract is not possible
    }
}
```

-   `Marker Interface` are empty interfaces
-   examples are Serializable, Cloneable and Remote

### Abstract Class

-   instance cannot be created
-   can be inherited
-   child have to implement all abstract methods

```
abstract class Name {}
```
