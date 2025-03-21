# GNU PRIVACY GUARD

1. generating keys

```
gpg --full-generate-key
```

2. generating revocation certificate

```
gpg --output ~/revocation.crt --gen-revoke <email>
```

3. key servers

```
gpg --keyserver pgp.mit.edu --search-keys <email>
```

4. verifying and signing a key

```
gpg --fingerprint <email>
gpg --sign-key <email>
```

5. sharing a public key

```
gpg --output foo.key --armor --export <email>
gpg --send-keys --keyserver pgp.mit.edu <fingerprint>
```

6. encrypting files

```
gpg --encrypt --sign --armor -r <email> <input>
gpg --decrypt <input.asc> > <output>
```

7. refreshing keys

```
gpg --keyserver pgp.mit.edu --refresh-keys
```

