# Pillars of OOPs

## Polymorphism

2 types in Java

### Overloading

- for method or constructor
- same class, different function signatures
- no, type and order of arguments
- return type doesn't count

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

- depends on the type of reference, not the object
- if not avaible, try to convert the parent reference

### Overriding

- for only method
- same function signatures, different class

## Inheritance

### Interface

- until java v1.7, non abstract methods are not supported.
- every variable is public static final
- every function is by default public abstract
- to prevent use `default` keyword

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

### Abstract Class

- instance cannot be created
- can be inherited
- child have to implement all abstract methods

```
abstract class Name {}
```
