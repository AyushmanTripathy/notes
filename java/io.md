# Input/Output

## Streams

-   are sequence of data (File, Console, Socket)
-   2 types of byte streams
    1. InputStream
    2. OutputStream
-   2 types of character streams
    1. Reader
    1. Writer
-   all 4 are abstract class

### Methods

-   all throw IOException
-   for inputs
    1. read()
    1. close
-   for outputs
    1. write() & overloads
    1. flush()
    1. close()

## Serialization

-   Serializable marker interface
-   writing to a steam
-   throws IOException

```java
FileOutputStream file = new FileOutputStream(filename);
ObjectOutputStream out = new ObjectOutputStream(file);
out.writeObject(obj);
```

-   reading from a stream
-   throws ClassNotFoundExpcetion, IOException

```java
FileInputStream file = new FileInputStream(filename);
ObjectInputStream in = new ObjectInputStream(file);

Name a = (Name) in.readObject()
```

## File

input classes are,

1. FileReader
1. FileWriter, read() -1 for EOF

buffered equivalents, made from reader and writer

1. BufferedReader, readLine()
1. BufferedWriter, newLine()

### RandomAccessFile

-   behaves like large array of bytes
-   if EOF is reached, EOFException (child of IOException)
-   can be created from File or filepath

```java
RandomAccessFile(File f, String mode)
RandomAccessFile(String path, String mode)

raf.seek(long pos) //change file pointer offset
```
