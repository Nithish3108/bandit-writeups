**Bandit Level 14 → Level 15 Write-up**

**Level Goal**



The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.



**Concepts Tested**



* Network communication basics
* Using nc (netcat) for TCP connections
* Understanding localhost and ports
* Client-server communication
* Reading passwords from /etc/bandit\_pass



**Solution**



Step 1: Connect to Bandit Level 14



SSH into the server using the SSH key from the previous level:



```bash ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220 ```



Or if you saved the password, use:



```bash ssh bandit14@bandit.labs.overthewire.org -p 2220 ```



Step 2: Get the Current Level Password



Read the password for bandit14 from the password file:



```bash cat /etc/bandit\_pass/bandit14 ```



Copy or note this password. You'll need to submit it to port 30000.



Step 3: Connect to Port 30000 Using Netcat



Use nc (netcat) to connect to localhost on port 30000:



```bash nc localhost 30000 ```



Or you can use telnet as an alternative:



```bash telnet localhost 30000 ```



Step 4: Submit the Password



After connecting, the service will wait for input. Type or paste the bandit14 password and press Enter.



The service will respond with the password for bandit15:

Correct!

[password_for_bandit15]





**password level 14-15:** #############################





