#linux #linux_commands #overthewire #bandits 
### **Level Goal**

The password for the next level is stored in a file named `readme` in the home directory. However, `.bashrc` has been modified to immediately log you out when you SSH into `bandit18`.

---
### **Method 1: Redirect Output to a World-Readable File**

Use SSH to execute a command that runs **before** `.bashrc` triggers, and save the output to a file in `/tmp`:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme > /tmp/banditpass18"
```

Then log in as a previous level (e.g., `bandit17`) and read the file:

```bash
cat /tmp/banditpass18
```

### **Why it works:**

- The command is executed **before** the shell is fully initialized.
    
- The file remains after you're booted out and can be accessed by any user.
    

---

### **Method 2: Use a Different Shell (Bypass `.bashrc`)**

You can spawn an interactive shell **other than bash** to avoid triggering `.bashrc`:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "sh -i"
```

Once inside:

```bash
cat readme
```

### **Why it works:**

- `.bashrc` only runs when a **bash** shell starts.
    
- Using `sh` avoids `.bashrc` entirely.
    

---

### **Helpful Reading Material**

- `man ssh`
    
- [SSH Command Execution Basics](https://www.ssh.com/academy/ssh/command)
    
- [Arch Wiki: Bash Configuration Files](https://wiki.archlinux.org/title/Bash#Configuration_files)
    

---

### **Next**

Move to **[[Bandit Level 19 → Level 20]]**, where you'll write to a file owned by another user. Time to get creative! ⚙️