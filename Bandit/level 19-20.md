**Bandit Level 19 → Level 20 Write-up**

**Level Goal**



To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit\_pass/bandit20), after you have used the setuid binary.



**Concepts Tested**



* Understanding setuid (SUID) binaries
* File permissions and privilege escalation
* Running programs as other users
* Linux security model



**Solution**



Step 1: Connect to Bandit Level 19



SSH into the server using the password from the previous level:



```bash ssh bandit19@bandit.labs.overthewire.org -p 2220 ```



Step 2: List Files in Home Directory



Check what files are present:



```bash ls -la ```



You'll see a file named bandit20-do with special permissions.



Step 3: Check File Permissions



Examine the file permissions closely:



```bash ls -l bandit20-do ```



You'll see something like:



-rwsr-x--- 1 bandit20 bandit19 14880 Oct 14 09:19 bandit20-do



Notice the s in -rwsr-x---. This is the setuid bit, meaning the program runs with the privileges of the file owner (bandit20), not the user executing it.



Step 4: Execute the Binary Without Arguments



Run the program to see how to use it:



```bash ./bandit20-do ```





Step 5: Use the Binary to Read the Password



The binary allows you to run commands as bandit20. Use it to read the password file:



```bash ./bandit20-do cat /etc/bandit_pass/bandit20 ```





**password level 19-20:** ##################################











