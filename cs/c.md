# C Programming Language

from:- https://learn-c.org

## STRINGS

-   initialize strings

```
char a[] = "your strings"; // array
char * a = "your strings"; // pointer
```

-   string functions are avaliable in string.h

| function       | description                     |
| -------------- | ------------------------------- |
| strlen(str)    | returns string length           |
| strcat(a,b)    | add b to a                      |
| strncat(a,b,i) | adds i letters of b at end of a |
| strcpy(a,b)    | copies b to a                   |
| strcmp(a,b)    | compares a to b (0 for equal)   |

## FUNCTIONS

-   functions should be first declared

```
int foo(int bar);
int main() {
    foo(1);
}
int foo(int bar) {
    return bar + 1;
}
```

-   void keyword for not returning
-   static keyword used to reduce scope
-   by default functions are global

```
static void foo(void);
```

## REFRENCING BY ARGUMENTS

-   give memory address as argument to a function

```
void inc(int * n) {
    (*n)++;
}
int n = 0;
inc(&n);
printf("%d",n) // gives 1
```

## STATIC VARIABLES

-   static keyword for increasing scope of variables
-   by default variables are local

```
int counter() {
    static int count = 0;
    count++;
    return count;
}
int main() {
    printf("%d ", counter());
    printf("%d ", counter());
    return 0;
}
```

-   returns number of times function is called.

## STRUCTURES

-   defining custom data types

```
struct point { int x; int y; };
struct point p;
p.x = 10; p.y = 5;
```

-   typedef are used to define custom type

```
typedef struct {
    char * brand;
    int model;
} vehicle;

vehicle mycar;
mycar.name = "Ford";
```

## POINTERS

-   is a integer variable holding memory address pointing to a value.

```
char * name = "John";
```

-   "John" is stored sequentially in memory,
-   name points to "J" (first char)
-   \0 is null terminator (value is 0)

```
const int * ptr; // can be changed
int * const ptr; // cannot be changed
```

## DEREFRENCING

-   getting the value stored at a memmory address
-   arrays are actually pointers
-   [] operator does derefrencing for arrays
-   does dereferencing for pointers
-   void \* cannot be derefrenced

```
int a = 1;
int * pointer = &a;
printf("%d",*pointer) // gives 1
*pointer += 1;
printf("%d",*pointer) // gives 2
```

## POINTERS TO STRUCTURES

-   can be done using two syntax

```
void move(point * p) {
    (*p).distance++;
}
void move(point * p ) {
    p -> distance++;
}
```

## ARRAYS

-   arrays can be simulated as

```
char * vowels = "AEIOU";
char p = &vowels;
vowels[1] == *(p + 1) //true
```

## DYNAMIC ALLOCATION

-   helps in storing data with out knowing its size

```
person * me = (person *) malloc(sizeof(person));
me -> name = "John";
```

-   me is a pointer, has just enough memory to store person struct
-   malloc function returns a `void pointer`
-   (person \*) is called typecasting (changes pointer's type)

```
free(me);
```

-   frees the memory
-   note: sizeof is not actual function

| function        | description                                 |
| --------------- | ------------------------------------------- |
| malloc(n)       | allocates n no of bytes with garbage values |
| calloc(n, m)    | allocates n \* m no of bytes with value 0   |
| realloc(ptr, n) | reallocates ptr to n no of bytes, copys     |

-   values over uninitiated values are garbage.

## FUNCTION POINTERS

-   we can call funtions by pointers

```
void (*p)(int);
p = &function_name;
(p)(1);
```

-   pass functions to functions

## STORAGE CLASSES

-   used to change visibillity and lifetime of a variable
-   **NOTE**: cannot get address of register, but can store ptrs in it

| name     | stored in    | init value     | scope                   | freed          |
| -------- | ------------ | -------------- | ----------------------- | -------------- |
| AUTO     | stack        | garbage values | within block            | end of block   |
| STATIC   | data segment | zero           | within block            | end of program |
| EXTERN   | data segment | zero           | global (multiple files) | end of program |
| REGISTER | cpu register | garbage values | within block            | end of block   |

## STDLIB FUNCTIONS

### stdio.h

| function              | return value                  |
| --------------------- | ----------------------------- |
| int printf(char \*, ) | returns no of chars printed   |
| int scanf(char \*, )  | returns no of inputed scanned |

## MISCS

-   the value of the expression (a=b) is the value of a after the expression has been evaluated
-   `void *` can be assigned any pointer

```
int a = a + 10; //valid
void * b = &a;  //valid
```
