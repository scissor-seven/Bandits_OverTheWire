#linux #linux_commands #bandits #overthewire
## Objective
Find a file that:
- Is **owned by user `bandit7`**
- Is **owned by group `bandit6`**
- Is **exactly 33 bytes** in size
## Steps

### 1️⃣ Login to Bandit 6

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

Use the password from Level 5.

### 2️⃣ Locate the file using `find`

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

#### Breakdown:

- `/` → Search from the root directory
    
- `-type f` → Search only files
    
- `-user bandit7` → File owner must be `bandit7`
    
- `-group bandit6` → File group must be `bandit6`
    
- `-size 33c` → File must be **exactly** 33 bytes (`c` = bytes)
    
- `2>/dev/null` → Redirects errors to `/dev/null` to ignore permission-denied messages ([Ref: Linux Redirections](https://chatgpt.com/c/67e242bd-6430-800c-8bd2-1e866fa312f6#))

### 3️⃣ Read the password

```bash
cat <file-path>
```

Replace `<file-path>` with the output from `find`.

## Key Takeaways

- **Ownership filtering**: `-user` and `-group` help target files based on ownership.
    
- **Size filtering**: `-size` allows precise size-based searches.
    
- **Permission errors**: Use `2>/dev/null` to suppress unwanted error messages.
## Next
[[Bandit Level 7 → Level 8]]