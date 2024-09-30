# String

-   String are immutable
-   StringBuffer and StringBuilder are mutable
-   Java has no operator overloading
-   exception is `+` for strings
-   content is identified by

```java
str.hashCode();
```

- String, StringBuffer, StringBuilder implement CharSequence

```
char[] ch= {'a', 'b'};
String s = new String(ch);
```

### String Constant Pool

- string literals are stored here
- separate from heap
- for duplicates same reference is passed
