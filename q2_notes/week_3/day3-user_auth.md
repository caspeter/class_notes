# User Authentication



 ![11-30-auth](/Users/CasPeterMac/workspace/class_notes/img/11-30-auth.JPG)



YAGNI - "You Ain't Going to Need It"

Security is huge and people overlook it

Passwords stored in plain text is HORRIBLE

#### RULES TO PASSWORDS:

- Never store passwords in plain text
- Always ask, do I really need to store this?

### Hashing algorithms

It is one way.

The hashes should all be the same size (character count) in the end

ex:

```
┌─────────────┐        ┌───────────────┐       ┌─────────────────────┐
│             │        │               │       │ 6e9c 620d cd31 6bf2 │
│     Fox     │        │ Cryptographic │       │ 9a37 bf6d 0be3 d685 │
│             │───────▶│ hash function │──────▶│ acfd 18be a7e6 d5a2 │
│             │        │               │       │ a697 1045 3961 0491 │
└─────────────┘        └───  sha256  ──┘       └─────────────────────┘

┌─────────────┐        ┌───────────────┐       ┌─────────────────────┐
│             │        │               │       │ ddad 2ab3 b2a8 f269 │
│     Fax     │        │ Cryptographic │       │ a001 bb26 a075 4a6b │
│             │───────▶│ hash function │──────▶│ 49ed f7ab 7ddb c953 │
│             │        │               │       │ 12fa 89c8 e19a b03e │
└─────────────┘        └───  sha256  ──┘       └─────────────────────┘

┌─────────────┐        ┌───────────────┐       ┌─────────────────────┐
│             │        │               │       │ 46b7 ffe0 588c ec9b │
│    Haxor    │        │ Cryptographic │       │ 80de a058 a448 a063 │
│             │───────▶│ hash function │──────▶│ 9be9 451e 99ea 89f6 │
│             │        │               │       │ 3899 67e1 bcfc 3672 │
└─────────────┘        └───  sha256  ──┘       └─────────────────────┘

```

The hash is stored with the user info, and that is your remembered password. 

the password fox will always give you that hash, but you can't take a hash and figure out the password

**No colissions**: there should never be the same hash for two different inputs

**Avalanche effect**: if you slightly change the input, the hash will drastically change

Never just store hashes!

So we salt the passwords

```
 pw          salt(random word)         newpassword        
gold         salty                      goldsalty  ==> hash the newpassword
```

The only two things stored are the salt and the hash of the new password

A new 'salt' is generated for each password

Passwords are the only thing that you should be ok with the process being a little slower, like a second

BCrypt

- good cryptographic hashing algorithm.
- Automatically generated salts
- Control over the computational complexity

`rounds = 8` = 2 to the 8th = ~40 hashes/sec

`bcrypt.hashSync(req.body.password,8)`

returns

`$2a$08$.jEA1FSMXOSQhLXrKkN9.k9gyad8xN6r76q01`

the salt is a certain number of characters in this hash, then at a certain point the hash becomes the password

to Compare

`bcrypt.compareSync(myPlaintextPassword, hash);`

bcrypt does this on the server side

