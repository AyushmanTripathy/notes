# Groff

### Compiling to PDF

-   `-tle` for tables
-   `-T` for output format

```
groff -ms -T pdf -tle in.ms > out.pdf
```

### Macros

| marco | function    |
| ----- | ----------- |
| .TL   | title       |
| .AU   | author      |
| .fam  | set font    |
| .NH   | new heading |

### Special characters

| ms     | meaning      |
| ------ | ------------ |
| \\[bu] | bullet point |

### Equations

```
.EQ
f(x) = sum from 1 to N {{ x sup 2 } over {n - 1}}
.EN

.EQ
cos theta + isin theta
.EN
```

### URLs

```
.pdfhref W -D "https://example.com" example site
```

