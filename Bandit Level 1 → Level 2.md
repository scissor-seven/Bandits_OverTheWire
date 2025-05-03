#linux #linux_commands #bandits #overthewire
## Level Goal
The password for the next level is stored in a file called ==**-**==, located in the home directory
## Steps
- After *ssh*, you need to *cat* the file but how? It has only a *' - '* as filename.
- In order to *cat* such file, you can use the below command.
```bash
cat < -
```
- Once done, this level is finished. Login to next level.
## Helpful Reading Material

- [Google Search for “dashed filename”](https://www.google.com/search?q=dashed+filename)
- [Advanced Bash-scripting Guide - Chapter 3 - Special Characters](http://tldp.org/LDP/abs/html/special-chars.html)

NEXT -> [[Bandit Level 2 → Level 3]]