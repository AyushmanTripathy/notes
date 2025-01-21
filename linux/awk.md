# AWK

text processing utility

```
awk -F ":" '{ print $n $m }' <filename>
```

print the nth and mth column of delimiter ":"  
if n == 0, prints every column

-   NF : number of column in current row
-   NR : number of current row

print with string between the columns

```
awk {print $1"string"$2}
```

## AWK WITH REGEX

selects rows with that regex  
ex: prints 1st column of rows starting with x

```
awk '/^x/ {print $1}'
```

| regex  | description                                                        |
| ------ | ------------------------------------------------------------------ |
| [ad]   | Selects a or d                                                     |
| [a-d]  | Selects any character a through d (a, b, c, or d)                  |
| [^a-d] | Selects any character except a through d (e, f, g, h…)             |
| (red)  | Parentheses indicate the enclosed letters must appear contiguously |
| \|     | Means or in the context of a grouped match                         |
| {n}    | Modifies the preceding set to mean exactly n times                 |
| {n,}   | Modifies the preceding set to mean n or more times                 |
| {n,m}  | Modifies the preceding set to mean between n and m times           |

### SUB() AND GSUB()

replace apple with nut

```
{ sub(/apple/, "nut", $1); print $1 }
```

-   sub -> only in one column
-   gsub -> every column of the row

### LENGTH()

returns lines that have greater than 7 characters

```
'length($0) > 7'
```

### IF()

print row if last column is lol

```
{ if($NF == "lol") print $0 }
```

### FOR()

loop from 1 to 10 and print the string

```
'BEGIN { for(i=1; i<=10; i++) print i," lol ", i}'
```

### CONDITIONALS

block is executed if the condition before it is true

```
'$1 == /^[b,c]/ {print $0}'
```

if first column matches regex print the line
