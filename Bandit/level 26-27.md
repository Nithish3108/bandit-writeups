**Bandit Level 26 → Level 27 Write-up**

**Level Goal**



Good job getting a shell! Now hurry and grab the password for bandit27!

The Situation



After completing level 25→26, you should have a bash shell as bandit26. If you don't have this yet, go back and complete the previous level first!



**Solution** 



Step 1: Get a Shell as Bandit26 (If Not Already There)



If you're not already in bandit26's shell, follow the previous level steps:



Make your terminal VERY small (3-5 lines)

From your local machine:



```bash ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220 ```



Press v when you see --More--



In Vi, type: :set shell=/bin/bash and press Enter

In Vi, type: :shell and press Enter



You should now have a bash prompt as bandit26.



Step 2: Check What Files Are Available



```bash ls ```



You'll see:



bandit27-do  text.txt



The file bandit27-do looks interesting!



Step 3: Check the File Type



```bash ls -la ```



You'll see something like:



-rwsr-x---  1 bandit27 bandit26 14880 Oct 14 10:00 bandit27-do



Notice the s in -rwsr-x---? This means it's a setuid binary that runs as bandit27!



Step 4: Test How the Binary Works



Run it without arguments to see what it does:



```bash ./bandit27-do ```



Output:

Run a command as another user.

 Example: ./bandit27-do id



It lets us run commands as bandit27!



Step 5: Use the Binary to Read Bandit27's Password



Since the binary runs as bandit27, we can use it to read bandit27's password:



```bash ./bandit27-do cat /etc/bandit_pass/bandit27 ```





**password level 26-27:** #################################





