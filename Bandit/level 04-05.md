**Bandit Level 4 → Level 5 Write-up**

**Level Goal**



The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the "reset" command.



**Concepts Tested**



* Identifying file types with file command
* Understanding human-readable vs binary data
* Working with multiple files
* Using wildcards in Linux





**Solution**



Step 1: Connect to Bandit Level 4

SSH into the server using the password from the previous level:



```bash ssh bandit4@bandit.labs.overthewire.org -p 2220 ```





Step 2: Navigate to the Directory

Change into the inhere directory:



```bash cd inhere ```





Step 3: List All Files

Check what files are present:



```bash ls ```



You'll see multiple files named -file00, -file01, -file02, etc.





Step 4: Check File Types

Since we need to find the human-readable file, use the file command to check all files at once:



```bash file ./* ```



The \* wildcard matches all files in the current directory, and ./ ensures the dash-prefixed filenames are handled correctly.



You'll see output like:

./-file00: data

./-file01: data

./-file02: data

./-file03: data

./-file04: data

./-file05: data

./-file06: data

**./-file07: ASCII text**

./-file08: data

./-file09: data

The file marked as "ASCII text" is the human-readable one (in this example, -file07).





Step 5: Read the Human-Readable File



Use cat to read the file:



```bash cat ./-file07 ```



**password level 4-5:** ############################





