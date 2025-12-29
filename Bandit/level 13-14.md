**Bandit Level 13 → Level 14 Write-up**

**Level Goal**



The password for the next level is stored in /etc/bandit\_pass/bandit14 and can only be read by user bandit14. For this level, you don't get the next password, but you get a private SSH key that can be used to log into the next level.



**Concepts Tested**



* SSH key-based authentication
* Understanding public/private key pairs
* Downloading files from remote servers using scp
* Using SSH with identity files
* Setting proper file permissions for SSH keys



**Solution**



Step 1: Connect to Bandit Level 13



SSH into the server using the password from the previous level:



```bash ssh bandit13@bandit.labs.overthewire.org -p 2220 ```



Step 2: Check the Home Directory



List the files in the home directory:



```bash ls ```



You'll see a file named sshkey.private.



Step 3: View the SSH Key



Examine the private key file:



```bash cat sshkey.private ```



You'll see it's an SSH private key starting with:



-----BEGIN RSA PRIVATE KEY-----



Now that you've confirmed the key file exists, you need to download it.



Step 4: Exit to Your Local Machine



Exit the SSH session to return to your local machine:



```bash exit ```



You should now be back at your local terminal prompt.



Step 5: Download the SSH Key to Your Local Machine



From your local machine, download the key using scp:



```bash scp -P 2220 bandit13@bandit.labs.overthewire.org:~/sshkey.private . ```



Breaking down the command:



1. scp                                                    -> Secure copy (file transfer over SSH)
2. -P 2220                                                -> Specify port (note: capital P for scp, lowercase p for ssh)
3. bandit13@bandit.labs.overthewire.org:~/sshkey.private  -> Source file location
4. .                                                      -> Current directory on your local machine (destination)



When prompted, enter the password for bandit13.



Step 6: Set Proper Permissions on the Key



SSH requires private keys to have restrictive permissions. Set the correct permissions on your local machine:


```bash chmod 600 sshkey.private ```



This ensures only you (the owner) can read and write the file.



Step 7: Use the SSH Key to Login as Bandit14



Now from your local machine, use the downloaded private key to connect to bandit14:



```bash ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220 ```



Breaking down the command:



1. ssh                                  -> SSH client command
2. -i sshkey.private                    -> Specify the identity file (private key)
3. bandit14@bandit.labs.overthewire.org -> Connect as user bandit14
4. -p 2220                              -> Use port 2220



You should now be logged in as bandit14 without needing a password!



Step 8: Read the Password for Bandit14



Now that you're logged in as bandit14, you can read the password file:



```bash cat /etc/bandit_pass/bandit14 ```



**password level 13-14:** #################################

