#linux #linux_commands #overthewire #bandits 
### **Objective**

Retrieve the password by submitting the current level's password to **port 30001** on `localhost` using **SSL/TLS encryption**.

---
### **Method 1: Using `openssl s_client`**

The `openssl s_client` command establishes an SSL/TLS connection to a remote service.

```bash
openssl s_client -connect localhost:30001
```

- `s_client` → Acts as a generic SSL/TLS client.
    
- `-connect localhost:30001` → Connects to `localhost` on **port 30001**.
    

Once connected, manually enter the password from **Level 15**, and the server will return the password for **Level 16**.

---
### **Method 2: Using `echo` to Automate Input**

To avoid manually typing the password, pipe it into `openssl`:

```bash
echo "<password>" | openssl s_client -connect localhost:30001
```

- `echo "<password>"` → Sends the password as input.
    
- `|` → Pipes the output to the next command.
    
- `openssl s_client -connect localhost:30001` → Establishes an SSL connection and submits the password.
    

Replace `<password>` with the actual **Level 15 password**.

---
### **Method 3: Using `ncat` (Alternative Approach)**

`ncat` can also establish encrypted SSL connections:

```bash
echo "<password>" | ncat --ssl localhost 30001
```

- `ncat` → Netcat with SSL/TLS support.
    
- `--ssl` → Enables SSL/TLS encryption.
    
- `localhost 30001` → Connects to `localhost` on port 30001.
    

---
### **Troubleshooting**

- If you see `DONE`, `RENEGOTIATING`, or `KEYUPDATE`, refer to the **"CONNECTED COMMANDS"** section in `man s_client`.
    
- Ensure **port 30001 is open** before connecting (`netstat -tuln` or `ss -tuln`).
    

---
### **Next**

Proceed to **[[Bandit Level 16 → Level 17]]**!