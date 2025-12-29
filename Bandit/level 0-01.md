**Bandit Level 0 → Level 1 Write-up**

**Level Goal**



The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH to log into that level and continue the game.



**Concepts Tested**



* SSH connection basics
* Linux command line navigation
* Reading file contents with cat
* Understanding home directory structure



**Solution**



Step 1: Connect to Bandit Level 0

First, establish an SSH connection to the Bandit server:

**```bash** ssh bandit0@bandit.labs.overthewire.org -p 2220 ```

When prompted, enter the password: bandit0



Step 2: Explore the Current Directory

Once logged in, check what files are in the current directory:

**```bash**  ls  ```

You should see a file named "readme".



Step 3: Read the File

Use the cat command to display the contents of the readme file:

**```bash** cat readme ```



**password level 0-1:** #############################





