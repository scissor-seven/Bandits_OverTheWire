#bandits #overthewire #linux #linux_commands #git #shell 
### Level Goal

There is a git repository located at:

```
ssh://bandit30-git@localhost/home/bandit30-git/repo
```

on port **2220**. Use the password for `bandit30` to access it.

Clone the repository and find the password for the next level.

---

### Commands You May Need

`git clone`, `git tag`, `git show`, `cat`, `ls`

---
### Step 1: Clone the Git Repository

```bash
git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo
```

When prompted, enter the password for `bandit30`.

---
### Step 2: Enter the Repository

```bash
cd repo
ls -la
```

You may find the repo mostly clean — just a README or empty working directory.

---
### Step 3: List All Tags

Check if any Git tags are set in the repository:

```bash
git tag
```

You might see something like:

```
secret
```

---
### Step 4: Show the Tag Content

Inspect the tag using:

```bash
git show secret
```

This should reveal the commit or annotated message containing the password for `bandit31`.

---

### Why This Works

- Tags are often used to mark important states in a project. In CTF-style challenges, they may hide flags or credentials.
    
- `git show <tag>` allows viewing the exact content attached to that tag, such as annotated messages or commit details.
    

---
### Helpful Reading Material

- [Git Tags — Git SCM Book](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
    
- `man git-tag`
    
- `man git-show`
    
- `man git-clone`
    

---
### Next:

[[Bandit Level 31 → Level 32]]