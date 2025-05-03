#linux #linux_commands #bandits #overthewire 
## Objective
The password for the next level can be retrieved by **submitting the current level’s password** to **port 30000 on localhost**.
## Steps

### 1️⃣ Login to Bandit 14

```bash
ssh -i /home/bandit13/sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

- `-i /home/bandit13/sshkey.private` → Uses the private key from Level 13.
    
### 2️⃣ Retrieve the Current Level’s Password

```bash
cat /etc/bandit_pass/bandit14
```

- This will output **Bandit 14’s password**, which must be sent to port 30000.
    
### 3️⃣ Submit the Password to Port 30000

#### **Method 1: Using Netcat (`nc`)**

```bash
echo "$(cat /etc/bandit_pass/bandit14)" | nc localhost 30000
```

- `nc localhost 30000` → Connects to **port 30000** on localhost.
    
- `echo "$(cat /etc/bandit_pass/bandit14)"` → Sends the password to the port.
    
#### **Method 2: Using Telnet**

```bash
telnet localhost 30000
```

- After connecting, **manually type** the password and press **Enter**.
    
#### **Method 3: Using OpenSSL (`s_client`)**

```bash
echo "$(cat /etc/bandit_pass/bandit14)" | openssl s_client -connect localhost:30000 -quiet
```

- `openssl s_client` → Used to **connect securely** to a server using **SSL/TLS**.
    
- `-connect localhost:30000` →
    
    - `localhost` = The **target machine** (itself).
        
    - `30000` = The **port number** to connect to (some service is listening here).
        
- `-quiet` → Makes it **less noisy** (hides extra SSL handshake details).
### 4️⃣ Retrieve the Password for Bandit 15

After submission, the response will display **the password for Bandit 15**.

---
## Key Takeaways

- **Ports** allow communication between networked applications.
    
- **Netcat (`nc`)** is a simple and powerful tool for sending/receiving data over TCP/UDP.
    
- **Alternative methods (`telnet`, `openssl s_client`)** can also be used for port-based interactions.
    
## Helpful Reading Material

- [How the Internet Works (YouTube)](https://www.youtube.com/watch?v=7_LPdttKXPc)
    
- [IP Addresses](https://en.wikipedia.org/wiki/IP_address)
    
- [Localhost](https://en.wikipedia.org/wiki/Localhost)
    
- [Ports](https://en.wikipedia.org/wiki/Port_\(computer_networking\))
	
- [Port (computer networking) on Wikipedia](https://en.wikipedia.org/wiki/Port_\(computer_networking\))
## Next

[[Bandit Level 15 → Level 16]]