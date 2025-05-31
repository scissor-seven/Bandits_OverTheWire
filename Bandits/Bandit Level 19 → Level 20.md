#linux #linux_commands #overthewire #bandits 
### **Level Goal**

Use the **setuid binary** in the home directory to retrieve the password for the next level, which is stored in:

```bash
/etc/bandit_pass/bandit20
```

---

### **Step 1: Logging In**

```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
```

Use the password from Level 18.

---

### **Step 2: List the Binary File**

```bash
ls -l
```

Expected output:

```
-rwsr-x--- 1 bandit20 bandit19 7320 May  7  2020 bandit20-do
```

### **Explanation:**

- `-rwsr-x---` → The `s` in `rws` means the binary has **setuid** permissions.
    
- It runs as the **file owner (bandit20)** regardless of who executes it.
    

---

### **Step 3: Understand the Binary**

Run the binary without arguments:

```bash
./bandit20-do
```

Expected output:

```
Run a command as another user.
Usage: ./bandit20-do <command>
```

---

### **Step 4: Execute the Command to Read the Password**

Use the binary to run `cat` as the bandit20 user:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

This will output the **password for Level 20**.

---

### **Helpful Reading Material**

- [Setuid – Wikipedia](https://en.wikipedia.org/wiki/Setuid)
    

---

### **Next**

Move on to **[[Bandit Level 20 → Level 21]]**, where you'll be setting up network communication between two programs. 🛰️