**Bandit Level 20 → Level 21 Write-up**

**Level Goal**



There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).



NOTE: Try connecting to your own network daemon to see if it works as you think.



**Concepts Tested**



* Network listening with nc (netcat)
* Background processes in Linux
* Process communication over network sockets
* Using SUID binaries
* Client-server interaction



**Solution**



Step 1: Connect to Bandit Level 20



SSH into the server using the password from the previous level:



```bash ssh bandit20@bandit.labs.overthewire.org -p 2220 ```



Step 2: Check the Files



List files in the home directory:



```bash ls -la ```



You'll see suconnect, which is the setuid binary.



Step 3: Get the Current Level Password



Read the password for bandit20:



```bash cat /etc/bandit_pass/bandit20 ```



Copy this password—you'll need to send it through the network.



Step 4: Set Up a Listener on One Terminal



We need to create a server that listens on a port and sends the password. Use netcat to listen on a port (e.g., port 6000):



```bash echo "**********************************" | nc -l -p 6000 ```



Replace **************************************  with the actual bandit20 password.

Breaking down the command:



1. echo "password"  -> Output the password
2. |                -> Pipe to netcat
3. nc -l -p 6000    -> Listen on port 6000
4. -l               -> Listen mode
5. -p 6000          -> Port 6000







This will wait for a connection. Keep this running.



Step 5: Connect Using the SUID Binary (New Terminal/Session)



Open a second SSH session to bandit20 in another terminal:



```bash ssh bandit20@bandit.labs.overthewire.org -p 2220 ```



Now run the suconnect binary to connect to your listener:





```bash ./suconnect 6000 ```





Submit the current level password once the password is correct in the listener side you get the next level password.





**password level 20-21:** ##############################









