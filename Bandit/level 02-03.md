**Bandit Level 2 → Level 3 Write-up**

**Level Goal**



The password for the next level is stored in a file called "--spaces in this filename--" located in the home directory.



**Concepts Tested**



* Handling filenames with spaces
* Escape characters in Linux
* Tab completion in the shell
* Quoting methods for filenames



**Solution**



Step 1: Connect to Bandit Level 2

SSH into the server using the password from the previous level:



```bash ssh bandit2@bandit.labs.overthewire.org -p 2220 ```





Step 2: List Directory Contents

Check what files are present:

```bash ls ```

You'll see a file named "--spaces in this filename--".



Step 3: Understanding the Problem

If you try to read the file like this:



```bash cat --spaces in this filename-- ```



""" This won't work! Linux interprets each space-separated word as a different argument, so it tries to read four separate files: spaces, in, this, and filename. """





Step 4: Read the File

The correct way to read this file is:

```bash cat ./"--spaces in this filename--" ```



**password level 2-3:** ###############################







