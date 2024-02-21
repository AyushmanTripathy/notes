Modulo
------

- MOD is slower that other arithmatic operations

```c
int ans = (a+b) % MOD;
int ans = (long long) a * b % MOD;
```

- subtraction

```c
int ans = (a - b) % MOD;
if (ans < 0) ans += MOD;
```

- divide, using eucler's theorem
- here we assume MOD to be prime

```c
int ans = a * pow(b, MOD - 2) % MOD;
```
