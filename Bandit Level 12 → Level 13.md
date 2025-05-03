#linux #linux_commands #bandits #overthewire 
## Objective

The password for the next level is stored in `data.txt`, which is a **hexdump of a file that has been repeatedly compressed**. We need to:

1. Convert the hex back into a binary file.
    
2. Extract it step by step.
    
It’s best to work in a **temporary directory** to avoid clutter.

## Steps

### 1️⃣ Login to Bandit 12

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

Use the password from Level 11.

### 2️⃣ Create a Temporary Working Directory

```bash
mkdir -p /tmp/$(mktemp -d)
cd /tmp/$(ls -t | head -n 1)
```

- `mktemp -d` → Creates a **unique temporary directory**.
    
- `cd` into the newly created directory.
    
### 3️⃣ Copy and Rename `data.txt`

```bash
cp ~/data.txt ./
mv data.txt hexdump.txt
```

- `cp ~/data.txt ./` → Copies the file to the working directory.
    
- `mv data.txt hexdump.txt` → Renames it to indicate it's a **hex dump**.
    
### 4️⃣ Convert Hex to Binary

```bash
xxd -r hexdump.txt > extracted.bin
```

- `xxd -r` → Reverses the hex dump back into a binary file.
    
### 5️⃣ Identify File Type

```bash
file extracted.bin
```

- This tells us the **compression format** used.
    
### 6️⃣ Extract the File Step by Step

Since the file is **compressed multiple times**, repeat these steps until it’s fully extracted:
#### **Extraction Methods Based on File Type**

|File Type|Command to Extract|
|---|---|
|`gzip`|`mv extracted.bin extracted.gz && gunzip extracted.gz`|
|`bzip2`|`mv extracted.bin extracted.bz2 && bzip2 -d extracted.bz2`|
|`xz`|`mv extracted.bin extracted.xz && unxz extracted.xz`|
|`tar archive`|`tar -xf extracted.bin`|
|`POSIX tar archive`|`tar -xvf extracted.bin`|

After each extraction, **rerun `file extracted.bin`** to determine the next step.

### 7️⃣ Read the Password

Once `file extracted.bin` finally shows **ASCII text**, read the password:

```bash
cat extracted.bin
```

---
## Key Takeaways

- **Use `xxd -r`** to convert a hex dump back into a binary file.
    
- **Create a temporary working directory** to keep things organized.
    
- **Always check file type after each step** using `file extracted.bin`.
    
- **Repeated compression needs multiple extractions** until reaching readable text.
    
## Helpful Reading Material

- [Hex dump on Wikipedia](https://en.wikipedia.org/wiki/Hex_dump)
    
- [file](https://manpages.ubuntu.com/manpages/latest/man1/file.1.html)
    
- [xxd](https://manpages.ubuntu.com/manpages/latest/man1/xxd.1.html)
    
- [tar](https://manpages.ubuntu.com/manpages/latest/man1/tar.1.html)
    
- [gzip](https://manpages.ubuntu.com/manpages/latest/man1/gzip.1.html)
    
- [bzip2](https://manpages.ubuntu.com/manpages/latest/man1/bzip2.1.html)
    
- [mkdir](https://manpages.ubuntu.com/manpages/latest/man1/mkdir.1.html)
    
## Next

[[Bandit Level 13 → Level 14]]