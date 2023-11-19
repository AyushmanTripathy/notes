## John The Ripper

Three Modes

1. Single Crack Mode

- in crack.txt

```
<password>:<hash>
```

- the all variations in <password> is tried out

```
john --single --format=raw-sha1 crack.txt
```

2. Dictionary Mode

- we have the hash in crack.txt
- wordlist is used, by default john has a wordlist

```
john --wordlist=wordlist.txt --format=raw-sha1 crack.txt
```

3. Increament Mode

- not used as it checks for all possible combinations

#### User Passwords

- in linux, `/etc/shadow` have hashes

```
unshadow /etc/passwd /etc/shadow > output.db
john output.db
```

- in windows, `SAM` Database has hashes in LM format, we have to use
  `--format=lm`

- for zip or rar files, we use `zip2john` or `rar2john`
