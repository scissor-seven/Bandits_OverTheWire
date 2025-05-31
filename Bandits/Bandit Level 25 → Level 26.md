#bandits #overthewire #linux #linux_commands #vim #vi
### Level Goal

Logging in to `bandit26` from `bandit25` should be straightforward — but there’s a twist. The login shell for `bandit26` is **not** `/bin/bash`, but a restricted binary that behaves differently. You need to identify how it works and exploit its behavior to break out and retrieve the password.

---

### Commands You May Need

`ssh`, `cat`, `file`, `strings`, `ls`, `grep`, `echo`, `stty`, `reset`, `export`, `less`, `more`

---

### Key Details

- You have SSH access to `bandit26`.
    
- However, `bandit26` uses a **non-standard shell** — likely `/usr/bin/showtext`.
    
- You can exploit the terminal’s behavior to escape its restricted environment.
    

---

### Step 1: Identify the Login Shell

From `bandit25`, run:

```bash
grep bandit26 /etc/passwd
```

Example output:

```
bandit26:x:1026:1026::/home/bandit26:/usr/bin/showtext
```

This confirms that the login shell is a restricted binary — not a standard shell.

---

### Step 2: Resize Your Terminal Before Logging In

Reduce your terminal window size before running the following SSH command. This forces the restricted shell to page its output using `more`, placing it in interactive mode.

Then run:

```bash
ssh bandit26@localhost -p 2220
```

Because the terminal size is small, `more` will kick in — allowing interactive commands.

---

### Step 3: Break Out Using `more`

Once inside the `more` prompt:

1. Press `v` to open the `vi`/`vim` editor (many systems allow this as a fallback editor).
    
2. Inside `vi`, use the following command:
    

```bash
:set shell=/bin/bash
:shell
```

You’ll now drop into a Bash shell with root privileges of `bandit26`.

Now, retrieve the password:

```bash
cat /etc/bandit_pass/bandit26
```

---

### Alternative Method: Inspect the Binary

If `more` doesn’t trigger due to terminal size, or if it behaves differently, you can inspect the shell binary manually:

```bash
file /usr/bin/showtext
strings /usr/bin/showtext
```

This might reveal fallback behavior, allowed commands, or internal mechanics.

You can also try this classic vi shell escape manually from inside any editor:

```bash
:set shell=/bin/bash
:shell
```

---

### Explanation of Key Concepts

- **Restricted Shells:** Using `more` or `less` inside a script can invoke interactive behavior when terminal height is small.
    
- **Editor-Based Escapes:** Editors like `vi` or `vim` often have shell access as a feature, making them a gateway out of restricted environments.
    
- **Custom Shells & Binaries:** These can be reverse-engineered or behaviorally analyzed to understand weaknesses.
    

---

### Helpful Reading Material

- [Escape from Vim — StackOverflow](https://stackoverflow.com/questions/8489542/how-to-call-shell-commands-from-vim)
    
- [Login Shells — Wikipedia](https://en.wikipedia.org/wiki/Login_shell)
    
- `man more`
    
- `man vim`
    
- `man stty`
    

---

### Next:

[[Bandit Level 26 → Level 27]]