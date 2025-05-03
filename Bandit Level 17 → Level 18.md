#linux #linux_commands #overthewire #bandits 
### **Level Goal**

There are two files in the home directory:

- `passwords.old`
    
- `passwords.new`
    

The password for the next level is the **only line that differs** between the two files.

---

### **Step 1: Logging In**

```bash
ssh bandit17@bandit.labs.overthewire.org -p 2220
```

Use the password from Level 16.

---

### **Step 2: Checking Available Files**

```bash
ls
```

Expected output:

```
passwords.new  passwords.old
```

---

### **Step 3: Using `diff` to Find the Difference**

```bash
diff passwords.old passwords.new
```

**Explanation:**

- `diff` → Compares two files line by line and shows differences.
    
- Output will indicate which line is **added or changed** in `passwords.new`.
    

Example output:

```
42c42
< abcdefghijklmnop
---
> 5e8dd316726b0330
```

The line starting with `>` is the **password for Level 18**.

---

### **Helpful Reading Material**

- `man diff`
    
- [GNU Diff Utilities Manual](https://www.gnu.org/software/diffutils/manual/)
    

---

### **Next**

Proceed to **[[Bandit Level 18 → Level 19]]** — where you’ll deal with restricted shells. Get ready for a creative escape. 🛡️