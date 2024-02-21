IMAGES
------

- img files can also be zip files
- for getting matadata of image

1. identify -verbose:  imagemagik
1. file: dimension, comment
1. strings: get all strings in a files

- use `binwalk` to see if it has a archive.
- use extract the files 

```
binwalk --extract --dd ".*" <filename>
```

ZSTEG
-----

read pixel values as ASCII, etc

```
zsteg -a <filename>
```

STEGHIDE
--------

- can be used for many file formats
- requires a passphrase

```
steghide info <filename>
```

- use `steghide extract -sf <filename>` to extract.

JPGS
----

- height and width of image can be changed to hide content
- use cyberchef, upload img and run `to hex`
- copy output and `from hex` and `render image`

```
// in JPG file

ff c0 00 11 08 02 22 02 09

ff c0 => SOFO Identifier 
00 11 => Length
08    => Data Presicion
02 22 => Height
02 09 => Width
```

GIT
---

1. showing the file

```
git show SHA:./path/to/file
```

2. browsing the files

```
git checkout SHA
```

ENCODING
--------

- base64 is most common, base32 is also there.
- HINT: Starting with Q or ending with =

```
echo "string" | base64 -d
```

- if scripting is required, js

```js
str.charCodeAt(index);      // in c, (int) str[index];
String.fromCharCode(num)    // in c, (char) num;

btoa(str)       // Encoding in Base 64 
atob(str)       // Decoding Base 64
```

- for getting the hex values, in nvim

```
:%!xxd
```

or

```
xxd <filename> | nvim
echo <string> | xxd -r
```

