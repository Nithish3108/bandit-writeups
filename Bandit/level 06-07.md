**Bandit Level 6 → Level 7 Write-up**

**Level Goal**



The password for the next level is stored somewhere on the server and has all of the following properties:



**owned by user bandit7**

**owned by group bandit6**

**33 bytes in size**





**Concepts Tested**



* Searching the entire filesystem with find
* Understanding file ownership (user and group)
* Handling permission denied errors
* Redirecting error messages





**Solution**



Step 1: Connect to Bandit Level 6

SSH into the server using the password from the previous level:



```bash ssh bandit6@bandit.labs.overthewire.org -p 2220 ```





Step 2: Search the Entire Server

Since the file is "somewhere on the server," we need to search from the root directory (/). Use find with the specified criteria:



```bash find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null ```





Breaking down the command:



1. /               -> Search from the root directory (entire filesystem)

2. -type f         -> Look for files only

3. -user bandit7   -> File is owned by user bandit7

4. -group bandit6  -> File is owned by group bandit6

5. -size 33c       -> File size is exactly 33 bytes

6. 2>/dev/null     -> Redirect error messages (like "Permission denied") to /dev/null to hide them



Without the 2>/dev/null, you'll see many "Permission denied" errors for directories you can't access.

The command will output something like:



**/var/lib/dpkg/info/bandit7.password**



Step 3: Read the File

Use cat to read the password file:



```bash cat /var/lib/dpkg/info/bandit7.password ```





**password level 6-7:** #################################





