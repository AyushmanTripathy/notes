# JDBC

Java DataBase Connectvity  
standard java api for independent connectvity

## Java drivers

type 1 is slowest, type 4 is fastest

### JDBC-ODBC bridge driver

- parially java
- db independent
- only for windows

### Native API driver

- parially java
- db dependent
- portable across os

### Network Protocol driver

- fully java
- no client side libraries are required

### Thin driver

- fully java
- driver depends on database

## Process

1. Register the driver class

```java
Class.forName("com.mysql.cj.jdbc.Driver")
```

1. Get a connection

```java
Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/coder", "username", "password")
```

1. Create a statement

```java
Statement smnt = con.createStatement();
```

1. Execute query

```java
int count = smnt.executeUpdate("update queries");
ResultSet rs = smnt.executeQuery("select queries");
while (rs.next())
    rs.getInt(1);
```


1. close the connection

### PreparedStatment

- query planed is saved by database engine
- discared once connection is closed

```java
PreparedStatment ps = con.prepareStatement("insert into movies(?, ?)")

ps.setInt(1, 100);
ps.setString(2, "ayush");

int count = ps.executeUpdate();
```

### CallableStatment

- executes stored prodecures

```java
conn.prepareCall("{ call procedureName(?) }");
```

### ResultSetMetaData

- provides info about result set

```java
ResultSetMetaData rsmd = rs.getMetaData();
```

- methods are,
    1. getColumnCount()
    1. getColumnName(int)
    1. getColumnType(int)
    1. isNullable(int)
    1. isAutoIncrement(int)
