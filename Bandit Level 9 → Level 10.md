#linux #linux_commands #bandits #overthewire 
## Objective
Find the password stored in `data.txt`, which is among the **few human-readable strings**, and is **preceded by multiple `=` characters**.
## Steps

### 1️⃣ Login to Bandit 9

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

Use the password from Level 8.

### 2️⃣ Solve Using Different Methods

#### **Method 1: Using `strings` (Easiest)**

```bash
strings data.txt | grep '='
```

- `strings` extracts readable text from a file.
    
- `grep '='` filters lines containing `=` to locate the password.
    

#### **Method 2: Using `grep` with Hex Encoding**

```bash
grep '==' data.txt
```

- Searches for lines containing `==` (assuming multiple `=` precede the password).
    

#### **Method 3: Using `xxd` (Hex Dump)**

```bash
xxd data.txt | grep '='
```

- `xxd` converts the file into a **hexadecimal dump**.
    
- `grep '='` looks for occurrences of `=` in the ASCII portion.
    

#### **Method 4: Using `base64` Decoding**

```bash
base64 -d data.txt | grep '='
```

- If `data.txt` were base64-encoded, this would decode and search for `=`.
    

#### **Method 5: Using `tr` (Translate Characters)**

```bash
tr -cd '[:print:]' < data.txt | grep '='
```

- `tr -cd '[:print:]'` removes **non-printable characters**.
    
- `grep '='` searches for lines containing `=`.
    

#### **Method 6: Using `tar` (Archive Check)**

```bash
tar -tf data.txt | grep '='
```

- Lists archive contents (if `data.txt` is an archive) and filters for `=`.
    

#### **Method 7: Using `gzip`/`bzip2` (Compressed File Check)**

```bash
gzip -dc data.txt | grep '='
bzip2 -dc data.txt | grep '='
```

- Decompresses `data.txt` (if applicable) before searching for `=`.
    

#### **Method 8: Using `sort` + `uniq` (Redundancy Check)**

```bash
strings data.txt | sort | uniq -c | grep '='
```

- `sort | uniq -c` counts occurrences of each line.
    
- `grep '='` filters relevant lines.
    

#### **Method 9: Using `man` (Manual Reference for `strings`)**

```bash
man strings
```

- Opens the manual for `strings` to explore advanced options.
---
## Key Takeaways

- **`strings`** is the quickest way to extract readable text from binary files.
    
- **Binary data often contains hidden information**, so knowing how to extract it is crucial.
    
- **Understanding file encoding and compression helps in challenges like this.**
    

## Helpful Reading Material

- [strings](https://manpages.ubuntu.com/manpages/latest/man1/strings.1.html)
    
- [grep](https://manpages.ubuntu.com/manpages/latest/man1/grep.1.html)
    
- [xxd](https://manpages.ubuntu.com/manpages/latest/man1/xxd.1.html)  
## Next

[[Bandit Level 10 → Level 11]]
