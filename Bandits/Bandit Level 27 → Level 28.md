#bandits #overthewire #linux #linux_commands #git #shell 
### Level Goal

There is a git repository at:

```
ssh://bandit27-git@localhost/home/bandit27-git/repo
```

accessible on port **2220**. The password for `bandit27-git` is the same as for `bandit27`.

Your task is to **clone the repository** and find the password for the next level.

---
### Commands You May Need

`git clone`, `git log`, `git show`, `cat`, `ls`

---
### Step 1: Clone the Repository

Clone the remote git repository using SSH and the correct port:

```bash
git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
```

- When prompted for the password, enter the password you obtained for `bandit27`.
    

---
### Step 2: Inspect the Repository

Navigate into the cloned repository:

```bash
cd repo
ls -la
```

You may see a README or similar file. Try reading it:

```bash
cat README
```

If no password is there, check for commit history.

---
### Step 3: Review Git Commit History

Check the git logs:

```bash
git log
```

This shows the commit history. Look for a commit message that may hint at a password or change.

You’ll see something like:

```
commit 92f9dd... (HEAD -> master)
Author: someuser
Date: some date

    Initial commit of README file
```

Copy the commit hash and view its content:

```bash
git show <commit_hash>
```

Look closely at the diff or any file that might contain the password.

---
### Step 4: Recover the Password

If the password isn’t in the latest commit, check previous commits or untracked files.

```bash
git log
```

```bash
git show <older_commit_hash>
```

Eventually, you’ll find a commit containing the password for `bandit28`.

---
### Explanation of Key Concepts

- **Git clone via SSH:** Cloning from a remote server using SSH access.
    
- **Commit History (`git log`)**: Allows you to trace past changes, useful for recovering overwritten or deleted content.
    
- **Viewing Commits (`git show`)**: Lets you inspect the content of previous commits in full detail.
    

---
### Helpful Reading Material

- [Git - Basic Commands](https://git-scm.com/docs)
    
- [SSH in Git](https://www.git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server)
    
- `man git-clone`
    
- `man git-log`
    
- `man git-show`
    

---
### Next:

[[Bandit Level 28 → Level 29]]