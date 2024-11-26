# Access Modifiers

used to alter scope

1. DEFAULT, within the package
1. PRIVATE, within the class only
1. PROTECTED, within different package through subclasses
1. PUBLIC, no restriction

- private and protected are applied to class members

## Package

-   just directories
-   naming convention is reverse order of domain names
-   class containing main method is outside of the package

-   subpackages are same as unrelated packages used for organisation

```
javac -d <classes>
java -classpath <classes>
```

- **classpath** can be set as enviroment variable
- used by class loaders to find .class files   

- every class is part of some package
- if no package is specified -> **special unnamed package**

### static imports

-   import public static members of a class
-   use without class name

```java
import static java.lang.System.*;
out.println();
```

### name conflicts

-   importing class with same name from both packages
-   more specific import has priority
-   full package name can also be used

```java
import java.util.*;
import java.sql.Date;
Date d;             //refers to java.sql.Date, not java.util.Date
java.util.Date d;
```
