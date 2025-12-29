**Bandit Level 3 → Level 4 Write-up**

**Level Goal**



The password for the next level is stored in a hidden file in the inhere directory.



**Concepts Tested**



* Understanding hidden files in Linux
* Using ls with flags/options
* Navigating directories with cd
* File naming conventions in Unix-like systems



**Solution**



Step 1: Connect to Bandit Level 3

SSH into the server using the password from the previous level:

```bash ssh bandit3@bandit.labs.overthewire.org -p 2220 ```



Step 2: List Directory Contents

Check what's in the home directory:



```bash ls ```



You'll see a directory named "inhere".





Step 3: Navigate to the Directory



Change into the inhere directory:



```bash cd inhere ```





Step 4: List All Files



If you use a regular ls command, you won't see any files. This is because the file is hidden. In Linux, files starting with a dot (.) are hidden by default.



To see hidden files, use the -a flag (all):



```bash ls -a ```



You'll see output like:

.  ..   ...Hiding-From-You



The . represents the current directory, .. represents the parent directory, and ...Hiding-From-You is the hidden file containing the password.



Step 5: Read the Hidden File



Use cat to read the contents:



```bash cat ..Hiding-From-You ```



**password level 3-4:** #############################





