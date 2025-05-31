#linux #linux_commands #overthewire #bandits 
### **Level Goal**

The credentials for the next level can be retrieved by submitting the password of the current level to a port on `localhost` in the range **31000 to 32000**. Only one of these ports is correct:

- Some ports have no servers listening.
    
- Some will echo back your input.
    
- Only one port running over **SSL/TLS** will return the password for Level 17.
    
---
### **Step 1: Logging In**

Connect to the Bandit server as user `bandit16`:

```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

Use the password obtained from Level 15.

---
### **Step 2: Scanning Open Ports**

Use `nmap` to scan for open ports in the given range:

```bash
nmap -p31000-32000 localhost
```

**Explanation:**

- `nmap` → Network mapping utility to find open ports.
    
- `-p31000-32000` → Port range to scan.
    
- `localhost` → Target machine (your own in this case).
    

---

### **Step 3: Testing Open Ports (One Command at a Time)**

#### **Command: `telnet`**

```bash
echo "<password>" | telnet localhost <port>
```

- Used to test plain TCP connections.
    
- Replace `<port>` with each open port.
    

#### **Command: `nc` (netcat)**

```bash
echo "<password>" | nc localhost <port>
```

- Another plain TCP connection tool.
    

#### **Command: `ncat` (netcat with SSL support)**

```bash
echo "<password>" | ncat --ssl localhost <port>
```

- Adds SSL layer to the connection.
    

#### **Command: `socat`**

```bash
echo "<password>" | socat - OPENSSL:localhost:<port>
```

- A more flexible tool for creating network connections.
    

#### **Command: `openssl s_client`**

```bash
echo "<password>" | openssl s_client -connect localhost:<port> -quiet
```

- Use this to detect the SSL/TLS port.
    
- `-quiet` suppresses unnecessary output.
    

> Test each open port using these commands one at a time. The correct port will respond with the password for the next level.

---
### **Step 4: Extract the Password**

Once the correct port is found using the appropriate SSL/TLS-enabled command, the returned output will contain the **Level 17 password**.

Copy and save it.

---
### **Helpful Note**

If you see messages like `DONE`, `RENEGOTIATING`, or `KEYUPDATE`, read the **CONNECTED COMMANDS** section in:

```bash
man openssl-s_client
```

---

### **Helpful Reading Material**

- [Port scanner on Wikipedia](https://en.wikipedia.org/wiki/Port_scanner)
    
---

### **Next**

Proceed to **[[Bandit Level 17 → Level 18]]**, where you'll learn to escape restricted shells and elevate your control. ⚔️