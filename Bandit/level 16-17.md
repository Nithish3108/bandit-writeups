**Bandit Level 16 → Level 17 Write-up**

**Level Goal**



The password for the next level is not a normal password, but an SSH private key.

This key can be obtained by connecting to the correct SSL-enabled service running on localhost between ports 31000–32000.

The key must then be used from the local machine to log in as bandit17.



**Concepts Tested**



* Port scanning with nmap
* Identifying SSL-enabled services
* Using ncat with SSL
* SSH private key authentication
* Secure file transfer using scp
* Correct SSH key permissions



**Solution**



Step 1: Connect to Bandit Level 16



Login using the password from Level 15:



```bah ssh bandit16@bandit.labs.overthewire.org -p 2220 ```



Step 2: Scan for Open Ports



Scan ports 31000–32000 on localhost:



```bash nmap -p 31000-32000 localhost ```





From the results, identify the open port that accepts SSL connections.

The correct port is 31790.





Step 3: Connect to the SSL Service



Use ncat with SSL:



```bash ncat --ssl localhost 31790 ```





Step 4: Submit the Password



Paste the bandit16 password and press Enter.



If correct, the service returns an SSH private key:



-----BEGIN RSA PRIVATE KEY-----

...

-----END RSA PRIVATE KEY-----





Step 5: Save the Private Key on the Remote Server



Create a temporary file and paste the key:



```bash nano /tmp/bandit17.key ```





Save and exit.





Step 6: Fix File Permissions (Remote)



Set correct permissions:



```bash chmod 600 /tmp/bandit17.key ```



⚠️ Important Note



You cannot SSH as bandit17 from inside the Bandit server.

The private key must be downloaded to your local machine and used from there.





Step 7: Download the Key to Local Machine



From your local host, run:



```bash scp -P 2220 bandit16@bandit.labs.overthewire.org:/tmp/bandit17.key . ```





Enter the bandit16 password when prompted.





Step 9: Login as Bandit17 Using the Key



Now log in from your local machine:





```bash ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220 ```





You should log in without a password prompt.





Step 10: Get the Password for Bandit17



Once logged in:



```bash cat /etc/bandit_pass/bandit17 ```







**password level 16-17:** #################################





