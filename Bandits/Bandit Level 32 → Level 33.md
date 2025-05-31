#bandits #overthewire #linux #linux_commands #git #shell 
### Level Goal

After all your hard work, Bandit32 sends you off with a parting gift: a private SSH key to log into the final level. You’ll find the key in the **`/home/bandit32/sshkey.private`** file.

---
### Commands You May Need

`chmod`, `ssh`

---
### Step 1: View the Private Key File

Log in as `bandit32` and check the location:

```bash
ls -l /home/bandit32/sshkey.private
cat /home/bandit32/sshkey.private
```

You should see a PEM-encoded private key. Save this key content into a new file locally if you're testing it outside the server, or continue from inside the current level.

---
### Step 2: Set Correct Permissions

To use an SSH private key securely, you must change its permissions:

```bash
chmod 600 sshkey.private
```

If the key is stored outside the remote machine, make sure to do this on your local system.

---
### Step 3: SSH into Bandit33

Use the private key to login to Bandit33:

```bash
ssh -i sshkey.private bandit33@localhost -p 2220
```

You’ll be logged in directly without a password prompt since you're using key-based authentication.

---
### Step 4: Enjoy the Win

Once logged in, you’ll see a congratulatory message from OverTheWire developers. You’ve successfully completed the entire Bandit wargame!

---
### Why This Works

- This final level tests your understanding of SSH key authentication and basic file permissions.
    
- By using `ssh -i`, you specify a custom identity file (private key), and by ensuring it's only readable by you (`chmod 600`), SSH considers it secure enough to use.
    

---
### Helpful Reading Material

- [SSH Key Authentication](https://www.ssh.com/academy/ssh/key)
    
- `man ssh`
    
- `man chmod`
    

---

### Final Thoughts

Congratulations on making it through all 33 levels! The skills you’ve built here form a strong foundation for more advanced security challenges like Narnia, Leviathan, or Krypton.

---

**Next:** Maybe try another wargame at OverTheWire or build something cool with your new skills!