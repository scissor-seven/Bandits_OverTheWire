#linux #linux_commands #bandits #overthewire 
## Objective
The password for the next level is stored in `data.txt`, but the contents are **base64-encoded**. We need to decode it.

## Steps

### 1️⃣ Login to Bandit 10

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

Use the password from Level 9.

### 2️⃣ Solve Using Different Methods

#### **Method 1: Using `base64` (Easiest)**

```bash
base64 -d data.txt
```

- `base64 -d` → Decodes the base64-encoded content of `data.txt`.
    

#### **Method 2: Using `cat` with `base64`**

```bash
cat data.txt | base64 -d
```

- `cat data.txt` → Reads the file.
    
- `| base64 -d` → Pipes the content into `base64 -d` for decoding.
    
#### **Method 3: Using `openssl`**

```bash
openssl base64 -d -in data.txt
```

- `openssl base64 -d` → Uses OpenSSL to decode the file.
    
- `-in data.txt` → Specifies input file.
    
#### **Method 4: Using `xxd` (Hex Representation Check)**

```bash
xxd data.txt | base64 -d
```

- `xxd` converts `data.txt` into hex.
    
- `base64 -d` decodes if the file is in base64 format.
    
#### **Method 5: Using `tr` (Handling Special Characters)**

```bash
cat data.txt | tr -d '\n' | base64 -d
```

- `tr -d '

#### **Method 6: Using** `**man**` **(Manual Reference for** `**base64**`**)**

```
man base64
```

- Opens the manual for `base64`, useful for exploring advanced options.
    
---
## Key Takeaways

- **Base64 encoding** is commonly used for data transfer and storage.
    
- `**base64 -d**` is the most efficient way to decode base64 content.
    
- **Different tools (**`**openssl**`**,** `**tr**`**,** `**xxd**`**)** can also be used for decoding.
    
## Helpful Reading Material

- [base64](https://manpages.ubuntu.com/manpages/latest/man1/base64.1.html)
    
- [openssl](https://manpages.ubuntu.com/manpages/latest/man1/openssl.1.html)
    
- [tr](https://manpages.ubuntu.com/manpages/latest/man1/tr.1.html)
    
## Next

[[Bandit Level 11 → Level 12]]