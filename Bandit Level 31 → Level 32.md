#bandits #overthewire #linux #linux_commands #git #shell 
### Level Goal

There is a git repository located at:

```
ssh://bandit31-git@localhost/home/bandit31-git/repo
```

on port **2220**. Use the password for `bandit31` to access it.

Clone the repository and retrieve the password for the next level.

---
### Commands You May Need

`git clone`, `git log`, `git reflog`, `git checkout`, `git show`, `cat`, `ls`

---
### Step 1: Clone the Git Repository

```bash
git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo
```

Enter the password for `bandit31` when prompted.

---

### Step 2: Navigate into the Repo

```bash
cd repo
ls -la
```

The working directory may appear minimal or empty.

---
### Step 3: Check Commit History

Start with a regular commit log:

```bash
git log
```

If nothing useful shows up, this may be a clue that data has been removed or altered.

---

### Step 4: Explore Reflog for Deleted Commits

Use Git’s reflog to view recent history and movements of HEAD:

```bash
git reflog
```

This may show a previous state such as:

```
HEAD@{1}: commit (initial): removed password
```

---
### Step 5: Checkout the Previous Commit

Get the commit hash and inspect it:

```bash
git checkout <commit_hash>
ls -la
cat README
```

You should find the password for `bandit32` inside one of the files.

---
### Why This Works

- Git’s **reflog** tracks all changes to HEAD and branches, even if commits have been discarded from the visible history.
    
- You can recover deleted or hidden data by exploring and checking out those previous references.
    

---
### Helpful Reading Material

- [Git Reflog](https://git-scm.com/docs/git-reflog)
    
- [Git Internals](https://git-scm.com/book/en/v2/Git-Internals)
    
- `man git-reflog`
    
- `man git-checkout`
    

---
### Next:

[[Bandit Level 32 → Level 33]]