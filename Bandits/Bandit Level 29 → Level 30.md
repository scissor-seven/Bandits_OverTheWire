#bandits #overthewire #linux #linux_commands #git #shell 
### Level Goal
There is a git repository located at:

```
ssh://bandit29-git@localhost/home/bandit29-git/repo
```

on port **2220**. Use the password for `bandit29` to access it.

Clone the repository and retrieve the password for the next level.

---
### Commands You May Need

`git clone`, `git branch`, `git checkout`, `git log`, `git show`, `cat`, `ls`

---
### Step 1: Clone the Git Repository

```bash
git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo
```

Enter the password for `bandit29` when prompted.

---
### Step 2: Navigate into the Repo

```bash
cd repo
ls -la
```

At first glance, it may appear minimal or empty.

---
### Step 3: Check for Available Branches

Use this to list all branches, including remote ones:

```bash
git branch -a
```

You’ll likely find something like:

```
remotes/origin/dev
```

---
### Step 4: Switch to the Relevant Branch

```bash
git checkout dev
```

Then list the files again:

```bash
ls -la
```

Check for a `README` or similar file and inspect it:

```bash
cat README
```

It should contain the password for `bandit30`.

---
### Why This Works

- Sensitive data is often hidden on non-default branches.
    
- Git allows full inspection of all branches even if the main working tree appears empty.
    
- Learning to branch-navigate is crucial for source code auditing.
    

---
### Helpful Reading Material

- [Git - Branches](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
    
- `man git-branch`
    
- `man git-checkout`
    

---
### Next:

[[Bandit Level 30 → Level 31]]