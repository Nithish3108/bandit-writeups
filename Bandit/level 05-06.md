**Bandit Level 5 → Level 6 Write-up**

**Level Goal**



The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:



**human-readable**

**1033 bytes in size**

**not executable**





**Concepts Tested**



* Using the find command with multiple criteria
* Understanding file permissions
* File size specifications
* Filtering search results



**Solution**



Step 1: Connect to Bandit Level 5

SSH into the server using the password from the previous level:



```bash ssh bandit5@bandit.labs.overthewire.org -p 2220 ```



Step 2: Navigate to the Directory

Change into the inhere directory:



```bash cd inhere ```



Step 3: Explore the Directory Structure

Check what's inside:



```bash ls ```



You'll see multiple subdirectories (maybehere00, maybehere01, etc.), each containing multiple files. Manually checking each would be tedious.



Step 4: Use Find Command with Criteria

Use the find command to search for a file matching all three criteria:



```bash find . -type f -size 1033c ! -executable ```



Breaking down the command:



1. .              -> Search in the current directory and subdirectories
2. -type f        -> Look for files (not directories)
3. -size 1033c    -> File size is exactly 1033 bytes (the 'c' stands for bytes/characters)
4. ! -executable  -> File is NOT executable (the ! negates the condition)



This will output something like:



**./maybehere07/.file2**



Step 5: Read the File

Use cat to read the file found:



```bash find cat ./maybehere07/.file2 ```





**password level 5-6:** ###############################





