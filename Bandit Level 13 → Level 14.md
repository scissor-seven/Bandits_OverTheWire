#linux #linux_commands #bandits #overthewire 
## Objective
The password for the next level is stored in `/etc/bandit_pass/bandit14`. To access it, we need to use the SSH private key stored in `sshkey.private`.
## Steps

### 1️⃣ Login to Bandit 13

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

Use the password from Level 12.

### 2️⃣ Use the Private Key to Access Bandit 14

#### **Method 1: Basic SSH Key Authentication**

```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

- `-i sshkey.private` → Uses the provided private key for authentication.
    
- **No password is required**, as authentication is done via the key.
    

#### **Method 2: If Key Permissions Are Too Open**

If the key’s permissions are too open, SSH will refuse to use it. Fix this by:

```bash
chmod 600 sshkey.private
```

- `chmod 600` → Restricts the key file’s permissions to be used securely.
    
### 3️⃣ Retrieve the Password for Bandit 14

Once logged in as `bandit14`, view the password:

```bash
cat /etc/bandit_pass/bandit14
```

---
## Key Takeaways

- **SSH keys** provide password-less authentication for secure access.
    
- **`chmod 600`** ensures private keys are secure and usable by SSH.
    
- **System passwords** for each level are stored in `/etc/bandit_pass/`.
    
## Helpful Reading Material

- [SSH Key Authentication](https://manpages.ubuntu.com/manpages/latest/man1/ssh-keygen.1.html)
    
- [chmod](https://manpages.ubuntu.com/manpages/latest/man1/chmod.1.html)
    
- [SSH/OpenSSH/Keys]([https://help.ubuntu.com/community/SSH/OpenSSH/Keys](https://help.ubuntu.com/community/SSH/OpenSSH/Keys))
    
## Next

[[Bandit Level 14 → Level 15]]