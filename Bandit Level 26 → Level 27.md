#bandits #overthewire #linux #linux_commands 
### Level Goal

*Good job getting a shell! Now hurry and grab the password for `bandit27`.*

---

### Commands You May Need

`ssh`, `cat`, `ls`, `chmod`, `file`, `strings`, `./<binary>`, `more`, `vi`, `echo`

---

### Key Details

- You’ll face the same restricted shell from the previous level (custom binary shell).
    
- Escape the shell using the same **terminal resize + interactive pager trick**.
    
- Once inside, a **binary file** in your home directory can be used to reveal the password.
    

---

### Step 1: Resize Terminal and Login

Before logging into bandit26, reduce your terminal size to a small number of rows (e.g., <3 lines). Then:

```bash
ssh bandit26@localhost -p 2220
```

This will cause the output to page using `more`, placing you in interactive mode.

---

### Step 2: Escape the Restricted Shell

1. When prompted by `more`, press `v` to open `vi`.
    
2. In vi, type:
    

```bash
:set shell=/bin/bash
:shell
```

You’ll now land in a bash shell with bandit26 privileges.

---

### Step 3: Locate and Investigate the Binary

```bash
ls -la
```

You should see a binary like:

```
-rwsr-x--- 1 bandit27 bandit26 7330 May  7 20:14 bandit27-do
```

This means the file is owned by `bandit27`, but can be executed by `bandit26` (you).

---

### Step 4: Execute the Binary to Read the Password

Try running the binary and observe how it behaves:

```bash
./bandit27-do
```

If it accepts a command, use:

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

The output will be the password for `bandit27`.

---

### Why This Works

- The binary has **setuid** permissions, so it runs with the privileges of its owner (`bandit27`).
    
- Executing `cat /etc/bandit_pass/bandit27` through it lets you read a file you otherwise wouldn’t have access to.
    

---

### Helpful Reading Material

- [Setuid on Wikipedia](https://en.wikipedia.org/wiki/Setuid)
    
- `man bash`
    
- `man more`
    
- `man vi`
    
- `man chmod`
    

---

### Next:

[[Bandit Level 27 → Level 28]]