#linux #linux_commands #bandits #overthewire 
## Objective

The password for the next level is stored in `data.txt`, but all **letters (a-z, A-Z) have been rotated by 13 positions (ROT13)**. We need to decode it.
## Steps

### 1️⃣ Login to Bandit 11

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

Use the password from Level 10.

### 2️⃣ Solve Using Different Methods

#### **Method 1: Using `tr` (Easiest)**

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

- `tr 'A-Za-z' 'N-ZA-Mn-za-m'` → Replaces letters with their ROT13 equivalent.
    
#### **Method 2: Using `sed`**

```bash
sed 'y/ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz/NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm/' data.txt
```

- `sed 'y/.../.../'` → Performs ROT13 transformation by replacing letters.
    
#### **Method 3: Using `awk`**

```bash
awk '{print gensub(/[A-Za-z]/, "&", "g", $0) | "tr A-Za-z N-ZA-Mn-za-m"}' data.txt
```

- Uses `awk` to apply `tr` for ROT13 conversion.
    
#### **Method 4: Using `python`**

```bash
python3 -c "import codecs; print(codecs.decode(open('data.txt').read(), 'rot_13'))"
```

- Uses Python's built-in **ROT13 decoder** to process the file.
    
#### **Method 5: Using `xxd` (Hex Check)**

```bash
xxd data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

- Converts file content to hex, then applies ROT13.
    
#### **Method 6: Using `man` (Manual Reference for `tr`)**

```bash
man tr
```

- Opens the manual for `tr`, useful for understanding text transformations.
    
---
## Key Takeaways

- **ROT13** is a simple substitution cipher shifting letters by 13 places.
    
- **`tr`** is the quickest way to decode ROT13 text.
    
- **Other tools (`sed`, `awk`, `python`)** provide alternative solutions.
    

## Helpful Reading Material

- [tr](https://manpages.ubuntu.com/manpages/latest/man1/tr.1.html)
    
- [sed](https://manpages.ubuntu.com/manpages/latest/man1/sed.1.html)
    
- [python codecs](https://docs.python.org/3/library/codecs.html)
    
## Next

[[Bandit Level 12 → Level 13]]