# Lua Programming langauge

from: [Programming in Lua](https://lua.org/pil/contents.html)

### Description

-   made in brazil
-   extension scritpting lanugague
-   garbage collected
-   keywords are used (no identation)
-   comments

```lua
-- single line commments
--[[
    multiline comments
--]]
```

## Variables

-   default value is `nil`
-   to delete a varibale assign it `nil`
-   reserved variables have the format

```lua
_NAME
```

-   by default variables have global scope
-   can be limited by `local` (does not work in interactive mode)

```lua
local a = 10
```

-   for more control on scope

```lua
do
    local a = 10
end
```

-   functions are first class and can be assigned to varibales

## Types

-   can be determined by `type` function

1. nil
1. boolean
1. number (double precision floating points)
1. string
1. userdata
1. function
1. thread
1. table

-   `0` and empty string are also true in lua
-   everything except for false and nil are true
-   convert using `tonumber` and `tostring`

### Strings

-   strings are immutable and modified through

```lua
string.gsub(a, "pattern", "replace_by")
```

-   strings are converted to numbers for arithmatic operators
-   formatted like that in c

```lua
string.format('name is %s, %s %s', "bond", "james", "bond")
```

-   string concatination is not `+` but is `..`
-   numbers given to `..` will be converted to strings

```lua
10 == "10"  -- false
```

-   `[[` or `[==[` can be used instead of quotes
-   `[[` are multiline and ignore first char if newline

### Tables

-   associative arrays (indexed by anything)
-   only data structuring mechanism
-   not value or varibale but objects
-   no declarations in lua
-   indicies as well as the values can be any type
-   set to `nil` to delete
-   variables are themselves stored as table

```lua
a = {}
a["x"] = 10
a.x = 10
```

-   iteration for integer arrays

```lua
for i, x in ipairs(a) do print(x) end
```

## Expressions

-   all arithmatic operators (`^` is not implemented)
-   all relational operators (`~=` is not equal)
-   logical operators are `not`, `and` and `or`

```lua
x = x or v      --equivalent to if (!x) x = v;
(a and b) or c  --equivalent to a ? b : c
```

-   no ternary operator
-   for table constructors

```lua
list = { "james", "bond" }
map = { first="james", last="bond" }
```

-   if key not passed, they are indexed

## Statements

-   mutiple assignments like python

```lua
x, y = y, z     --swapping
```

### Control structures

-   `if`, `elseif` and `else` for conditionals
-   `while cond do end` or `repeat unitll cond` for iteration
-   for is of two types

```lua
for i=1,10,2 do print(i) end    --loop for 1 to 10 by 2
for key in pairs(table) do print(key) end   --loop for all keys in table
```

-   no `continue`
-   `break` and `return` can only be at end of a block, workaround

```lua
do return end
```

## Function

- parenthesis are optional
- syntax to call func with obj as first parameter

```lua
obj:func(10)    --equivalent to obj.func(obj, 10)
```

- functions can return multiple values

```lua
function f(x) return x + 1, x * 2 end
a, b = f(x)
```

- the funciton call must be last 

```lua
a = {f(10)}         -- 11 20
a = {f(10), 10}     -- 11 10
```

- to force only one return value use `()`

```lua
a = (f(10))
```

- `unpack` to un pack values of array
- named arguments are not supported
- variable no of arguments

```lua
function f(a, b, ...)
    for i, v in ipairs(arg) do print(v) end
end
```

- functions are anonymous, they themsevles have no name.
- `print` is the name of the variable that stores the function
- lua has lexical scoping, inner functions have access to outer funtions

```lua
local function foo()        --syntactic sugar
local foo = function()      --equivalent
```

- none global functions are used for libraries

```lua
function lib.func() ... end
lib.func = function() ... end   --equivalent
```

- has `proper tail calls`, hence no limit on recursion
- here g(x) is the last action, info about calling function f(x) is not needed 
- after execution of g(x) returning to f(x) is not required 

```lua
function f(x)
    -- something
    return g(x)
end
```
