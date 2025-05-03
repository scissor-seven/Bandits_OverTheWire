#linux #linux_commands #bandits #overthewire
## Objective
Find the password stored in `data.txt`, which is the **only line that occurs once** in the file.
## Steps

### 1️⃣ Login to Bandit 8

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

Use the password from Level 7.
### 2️⃣ Solve Using Different Methods

#### **Method 1: Using `sort` + `uniq` (Easiest)**

```bash
sort data.txt | uniq -u
```

- `sort data.txt` → Sorts lines in alphabetical order.
    
- `uniq -u` → Filters out duplicate lines, leaving only unique ones.
#### **Method 2: Using `grep`**

```bash
grep -vxF -f <(sort data.txt | uniq -d) data.txt
```

- `sort data.txt | uniq -d` → Finds **duplicate** lines.
    
- `<(command)` → Creates a **temporary file-like input** from a command.
    
- `grep -vxF -f` → Filters out lines **matching** duplicates, printing only unique ones.
    
    - `-v` → Inverts the match (shows lines **not** in duplicates).
        
    - `-x` → Matches **whole** lines (not partial matches).
        
    - `-F` → Treats search patterns **literally** (no regex).
        
    - `-f <file>` → Takes patterns from a file (in this case, the process substitution).
        

#### **Method 3: Using `awk`**

```bash
awk '{count[$0]++} END {for (line in count) if (count[line] == 1) print line}' data.txt
```

- `awk` processes text line by line.
    
- `count[$0]++` → Creates an array where each **line** is counted.
    
- The `END` block runs **after all lines are processed**:
    
    - `if (count[line] == 1) print line` → Prints only lines that appear **once**.
        

#### **Method 4: Using `strings`**

```bash
strings data.txt | sort | uniq -u
```

- `strings` extracts **printable** text from a file (useful for binaries or mixed-content files).
    
- `sort | uniq -u` finds the unique line.
    

#### **Method 5: Using `tr`**

```bash
tr ' ' '\n' < data.txt | sort | uniq -u
```

- `tr ' ' '\n'` → Converts **spaces** into **new lines**, making each word a separate line.
    
- Sorting and filtering then isolates the unique one.
    

#### **Method 6: Using `xxd`**

```bash
xxd data.txt | sort | uniq -u
```

- `xxd` converts the file into a **hexadecimal dump** (hex + ASCII representation).
    
- Sorting and filtering still work on the ASCII portion of the dump.
    

#### **Method 7: Using `base64` (Encoded Check)**

```bash
base64 -d data.txt | sort | uniq -u
```

- `base64 -d` decodes the file assuming it's **base64 encoded**.
    
- Sorting and filtering find the unique line.
    

#### **Method 8: Using `tar` (Archive Check)**

```bash
tar -tf data.txt | sort | uniq -u
```

- `tar -tf` lists contents of an archive **if `data.txt` is actually an archive**.
    
- Sorting and filtering find unique entries.
    

#### **Method 9: Using `gzip`/`bzip2` (Compressed File Check)**

```bash
gzip -dc data.txt | sort | uniq -u
bzip2 -dc data.txt | sort | uniq -u
```

- `gzip -dc` / `bzip2 -dc` → **Decompress** the file and output readable content.
    
- Sorting and filtering find the unique line.
    

#### **Method 10: Using `man` (Manual Reference for `uniq`)**

```bash
man uniq
```

- Opens the **manual page** for `uniq` to explore advanced options.
---

## Key Takeaways

- **`sort | uniq -u`** is the most efficient way to find a unique line.
    
- **Text processing tools (`awk`, `grep`, `tr`)** help filter data efficiently.
    
- **Understanding how data is structured** is key to solving challenges faster.
    

## Helpful Reading Material

- [sort](https://manpages.ubuntu.com/manpages/latest/man1/sort.1.html)
    
- [uniq](https://manpages.ubuntu.com/manpages/latest/man1/uniq.1.html)
    
- [grep](https://manpages.ubuntu.com/manpages/latest/man1/grep.1.html)
    

## Next

[[Bandit Level 9 → Level 10]]