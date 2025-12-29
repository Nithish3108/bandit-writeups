**Bandit Level 15 → Level 16 Write-up**

**Level Goal**



The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption





**Concepts Tested**



* SSL/TLS encrypted connections
* Using ncat with SSL
* Secure communication vs plain text
* Understanding encrypted network services





**Solution**



Step 1: Connect to Bandit Level 15



SSH into the server using the password from the previous level:



```bash ssh bandit15@bandit.labs.overthewire.org -p 2220 ```



Step 2: Get the Current Level Password



Read the password for bandit15:



```bash cat /etc/bandit_pass/bandit15 ```





Copy or note this password carefully.



Step 3: Connect Using SSL 



Use ncat with SSL enabled to connect to port 30001:



```bash ncat --ssl localhost 30001 ```





This establishes an SSL/TLS encrypted connection to the service.



Step 4: Submit the Password



Once connected, paste the bandit15 password and press Enter.



The service will respond with:



Correct!

[password_for_bandit16]





**password level 15-16:** #################################





