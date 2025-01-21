## Passwords

1. Encrpted Passwords
    - passwords are encrypted with a key
    - ex: AES (Advanced Encryption Standard)
1. Hashing
    - hash is generated using a one way function
    - 2 strings can be compared by comparing their hash
    - ex: MD5, SHA1
1. Salting
    - Rainbow tables (common passwords along with their precomputed hash)
    - to prevent use of Rainbow tables, custom salt is added to passwords
    - salts are stored for each password
1. Slow Hashing
    - to prevent brute force
    - here hash functions are slow, to prevent brute forcing
    - ex: bcrypt, Aargon

### bcrypt

- cost can be increased to make it slower

```
$2a$12$R9h/cIPz0gi.URNNX3kh2OPST9/PgBkqquzi.Ss7KIUgO2t0jWMUW
\__/\/ \____________________/\_____________________________/
Alg Cost      Salt                        Hash
```

## OAuth
