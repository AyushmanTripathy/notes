# String

-   String are immutable
-   StringBuffer and StringBuilder are mutable
-   Java has no operator overloading
-   exception is `+` for strings
-   content is identified by

```java
str.hashCode();
```

-   String, StringBuffer, StringBuilder implement CharSequence

```
char[] ch= {'a', 'b'};
String s = new String(ch);
```

### String Constant Pool

-   string literals are stored here
-   separate from heap
-   for duplicates same reference is passed

```
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello");

s1 == s2 //true
s1 == s3 //false
```

## String

-   immutable
-   thread safe
-   highly performant, highly memory efficient
-   not syncronised

## StringBuffer

-   mutable
-   thread safe
-   less performant, less memory efficient
-   syncronised

## StringBuilder

-   mutable
-   not thread safe
-   performant, memory efficient
-   not syncronised

## StringTokenizer

- used to break string into tokens
- default delimiters are \s, \n, \t, `StringTokenizer(String s)`
- custom using `StringTokenizer(String s, String delim)`

```java
while (st.hasMoreTokens())
    st.nextToken()
```
