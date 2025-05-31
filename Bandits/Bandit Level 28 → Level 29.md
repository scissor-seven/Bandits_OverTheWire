#bandits #overthewire #linux #linux_commands #git #shell 
### Level Goal

There is a git repository located at:

```
ssh://bandit28-git@localhost/home/bandit28-git/repo
```

on port **2220**. Use the password for `bandit28` to access it.

Clone the repository and find the password for the next level.

---
### Commands You May Need

`git clone`, `git log`, `git show`, `git branch`, `git checkout`, `cat`, `ls`

---
### Step 1: Clone the Git Repository

```bash
git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
```

Provide the `bandit28` password when prompted.

---
### Step 2: Navigate into the Repo

```bash
cd repo
ls -la
```

You may notice that the working directory doesn’t reveal much at first glance.

---
### Step 3: Check for Branches

Sometimes, sensitive information is committed on other branches. Check existing branches:

```bash
git branch -a
```

You may find something like:

```
remotes/origin/dev
```

---
### Step 4: Switch to the Relevant Branch

```bash
git checkout dev
```

Now list the contents again:

```bash
ls -la
cat README
```

The `README` or another file in this branch should contain the password.

---
### Why This Works

- Git repositories often contain multiple branches. While `master` may look clean, secrets or sensitive history could reside in other branches.
    
- Knowing how to explore git metadata (like branches and history) gives you insight into a project's structure and hidden content.
    

---
### Helpful Reading Material

- [Git - Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
    
- `man git-branch`
    
- `man git-checkout`
    
- `man git-clone`
    

---
### Next:

[[Bandit Level 29 → Level 30]]