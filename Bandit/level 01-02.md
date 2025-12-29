**Bandit Level 1 → Level 2 Write-up**

**Level Goal**



The password for the next level is stored in a file called - located in the home directory.



**Concepts Tested**



* Handling files with special characters in their names
* Understanding how the dash (-) character is interpreted in Linux
* Using relative and absolute paths
* Alternative ways to read files



**Solution**



Step 1: Connect to Bandit Level 1

SSH into the server using the password from the previous level:

```bash ssh bandit1@bandit.labs.overthewire.org -p 2220 ```



Step 2: List Directory Contents

Check what files are present:

```bash ls ```

You'll see a file named -.



Step 3: Understanding the Problem

If you try to read the file using the standard approach:

```bash cat - ```



""" This won't work! The dash (-) is interpreted as stdin (standard input) by most Linux commands, not as a filename. The command will wait for keyboard input instead of reading the file. """





Step 4: Read the File Using a Path

To read a file named -, you need to specify it as a path. There are several methods:



Method 1: Using relative path with ./

```bash  cat ./- ```



Method 2: Using absolute path

```bash cat /home/bandit1/- ```



**password level 1-2:** ###########################





