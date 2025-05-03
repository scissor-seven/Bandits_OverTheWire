#linux #linux_commands #overthewire #bandits 
### 🌟 **Level Goal**

Use the `setuid` binary in the home directory. It connects to `localhost` on a specified port, expects the password for `bandit20`, and if correct, returns the password for `bandit21`.

---

### 🔹 **Approach:**

The binary's logic:

- You start a listener on `localhost` (using `nc`).
    
- The `setuid` binary connects to your listener.
    
- You send the old password.
    
- It replies with the new password.
    

---

### 🔧 **Commands & Steps:**

#### Step 1: Start a Listener with `nc`

```bash
nc -lvp <port_number>
```

- `nc`: Netcat, for creating TCP connections.
    
- `-lvp`: `-l` (listen mode), `-v` (verbose), `-p` (specify port).
    

Pick any port above 1024 (e.g., `4444`).

---

#### Step 2: Run the `setuid` Binary

```bash
./suconnect <port_number>
```

- Replace `<port_number>` with the one you used with Netcat.
    
- The binary connects to your listener and waits for input.
    

---

#### Step 3: Send the Password

When the binary connects to your `nc` listener, type:

```bash
<bandit20_password>
```

You should receive the password for `bandit21` in response.

---

### 🤔 **Alternate Method:**

If you wish to automate the sending process:

```bash
echo "<bandit20_password>" | nc -lvp <port_number>
```

This sends the password automatically upon connection.

---

### 🔹 **Other Useful Commands Mentioned in Level Description:**

#### `ssh`

Securely log into the Bandit server:

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
```

- `ssh`: Secure Shell, used to connect remotely over encrypted channels.
    

---

#### `cat`

Display file contents, especially for the password:

```bash
cat /etc/bandit_pass/bandit20
```

- `cat`: Concatenate and print file contents.
    

---

#### `bash`

Invoke a new shell session if needed:

```bash
bash
```

- Useful for nested sessions or isolated testing.
    

---

#### `screen` & `tmux`

Terminal multiplexers that allow you to run persistent or multi-windowed terminal sessions:

```bash
screen
```

or

```bash
tmux
```

- Perfect for handling multiple connections and processes during the level.
    

---

#### Unix Job Control (`bg`, `fg`, `jobs`, `&`, `CTRL-Z`)

- `&` to run a process in the background:
    

```bash
nc -lvp 4444 &
```

- `jobs`: Lists background jobs.
    
- `fg`: Brings the last backgrounded job to the foreground.
    
- `CTRL-Z`: Pause (suspend) the current process.
    
- `bg`: Resume a paused process in the background.
    

---

### 🤯 **Important Concepts:**

- **setuid binary**: Runs with the file owner's privileges (here: `bandit21`).
    
- **TCP connection flow**: Client-server relationship where you create the server using `nc` and the binary acts as a client.
    
- **Job Control**: Manage and switch between active and background jobs in a Linux terminal session.
    

---

### 🔍 **Helpful Reading Material:**

- [Netcat on Wikipedia](https://en.wikipedia.org/wiki/Netcat)
    
- [Setuid on Wikipedia](https://en.wikipedia.org/wiki/Setuid)
    
- [tmux — Official GitHub](https://github.com/tmux/tmux/wiki)
    
- [GNU Screen Manual](https://www.gnu.org/software/screen/manual/)
    
- `man nc`
    
- `man ssh`
    
- `man bash`
    
- `man jobs`
    
- `man fg`
    
- `man bg`
    

---

### ➡️ **Next:**

[[Bandit Level 21 → Level 22]]