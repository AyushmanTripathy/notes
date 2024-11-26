# Exception Handling

-   Exception is an event that disrupts the normal flow of the program.
-   It is an object which is thrown at runtime, child of Throwable
-   Throwable and all its childrens

## Types

-   In java, three types of exceptions

1. Checked Exception
    - all except RuntimeException and Error
    - need to be caught or declared
1. Unchecked Exception
    - RuntimeException and its childrens
    - not checked at compile step
1. Error
    - Error and its childrens
    - are irrecoverable

-   Throwable class can be used by `throw` and `throws`

```
Throwable
| - Exception
    | - IOException
    | - SQLException
    | - ClassNotFoundException
    | - RuntimeException
        | - ArithmeticException
        | - NullPointerException
        | - NumberFormatException
        | - IndexOutOfBoundException
| - Error
    | - StackOverflowError
    | - OutOfMemoryError
    | - AssertionError
```

## Try Catch Finally

-   cannot be one liners
-   try must have atleast one catch or finally
-   parent class must be caught after child class
-   finally is executed even if try returns
-   expression is evaluated but returned after finally

```java
try {
    return func();
} finally {
    //will be executed after func()
}
```

-   returning in finally will triumph

### Throw

-   used to raise exceptions

```java
throw new Throwable("bad things happened");
```

### Throws

-   used to declare exceptions that can be throwen

### User Defined Exception

-   class which inherits Throwable and its childrens
-   Error & RuntimeException are not unchecked, all others are checked
