#bandits #linux #linux_commands #overthewire #shell #scripting 
### Level Goal

A daemon is listening on port 30002 and requires the current level's password followed by a 4-digit PIN. You must brute-force the correct PIN and submit the credentials in the required format to retrieve the next password.

---

### Commands You May Need

`nc`, `for`, `echo`, `grep`, `cut`, `sleep`, `2>/dev/null`

---

### Key Details

- Service runs on `localhost` at **port 30002**.
    
- Format expected by the service:
    
    ```
    <password><space><4-digit PIN>
    ```
    
- You don’t need any rate-limiting delay unless otherwise noted.
    

---

### Step 1: Test Service Behavior with `netcat`

Before building a brute-force loop, it helps to manually connect and inspect how the service responds:

```bash
echo test | nc localhost 30002
```

This results in an error message indicating the required format. Based on the message returned, you can infer the expected input syntax:

```bash
echo "<password> 1234" | nc localhost 30002
```

This trial-and-error method helps confirm that the service wants a **password followed by a space and a 4-digit PIN**.

---

### Method 1: Brute-force using a loop and `nc`

```bash
for i in {0000..9999}; do
  echo "<password> $i";
done | nc localhost 30002
```

**Note:** This method may generate too much noise if the service prints error messages. You can silence those using:

```bash
(for i in {0000..9999}; do echo "<password> $i"; done | nc localhost 30002) 2>/dev/null
```

---

### Method 2: Filtering for Success Response

To avoid scrolling through all failed attempts:

```bash
(for i in {0000..9999}; do echo "<password> $i"; done | nc localhost 30002) 2>&1 | grep -v "Wrong"
```

This will hide the failed attempts and show only the correct one.

---

### Method 3: Slower but Controlled Brute-force

```bash
for i in {0000..9999}; do
  echo "<password> $i" | nc localhost 30002 2>/dev/null
  sleep 0.05
done
```

- Adds a delay to avoid flooding the service.
    

---

### Explanation of Key Components

- `for i in {0000..9999}`: Loops through all 4-digit numbers.
    
- `nc localhost 30002`: Opens a TCP connection to the service.
    
- `2>/dev/null`: Redirects stderr to avoid clutter.
    
- `grep -v` or `grep -v "Wrong"`: Filters out lines containing errors.
    

---

### Helpful Reading Material

- [Netcat — Wikipedia](https://en.wikipedia.org/wiki/Netcat)
    
- `man nc`
    
- Bash Redirection: `man bash`
    

---

### Next:

[[Bandit Level 25 → Level 26]]