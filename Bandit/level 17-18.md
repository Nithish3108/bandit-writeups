**Bandit Level 17 → Level 18 Write-up**

**Level Goal**



There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new.





**Concepts Tested**



* Comparing files with diff
* Understanding file differences
* Finding changes between two versions
* Working with text file comparison tools



**Solution**



Step 1: Connect to Bandit Level 17



SSH into the server using the password from the previous level:



```bash ssh bandit17@bandit.labs.overthewire.org -p 2220 ```





Step 2: List Files in Home Directory



Check what files are present:



```bash ls ```



You'll see two files:



passwords.old

passwords.new





Step 3: Compare the Files Using diff



Use the diff command to find differences between the two files:



```bash diff passwords.old passwords.new ```



The output will show something like:



42c42

< [old_password]

---

> [new_password]



This means:



Line 42 in the old file contains [old_password]

Line 42 in the new file contains [new_password]



The new password (the one with >) is the password for bandit18





Step 4: Identify the New Password



The line marked with > (greater than) is from passwords.new and contains the password for bandit18.





**password level 17-18:** ###############################

