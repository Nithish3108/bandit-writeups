**Bandit Level 25 → Level 26 Write-up**

**Level Goal**



Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

The Problem



When you try to login to bandit26, you see a cool banner and then immediately get kicked out. We need to find a way to stay logged in!



**Solution**



Step 1: Connect to Bandit25



From your local machine, connect to bandit25:



```bash ssh bandit25@bandit.labs.overthewire.org -p 2220 ```



Step 2: Check What Files Are Available



```bash ls ```



You'll see a file: bandit26.sshkey



This is an SSH key we need to login to bandit26!



Step 3: Check What Shell Bandit26 Uses



Before we download the key, let's understand the problem:



```bash cat /etc/passwd | grep bandit26 ```



Result:

bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext

Notice: Normal users have /bin/bash, but bandit26 has /usr/bin/showtext!



Step 4: What Does This "showtext" Do?



Let's read it:



```bash cat /usr/bin/showtext ```



You'll see:



bash#!/bin/sh

export TERM=linux

exec more ~/text.txt

exit 0



Translation:



It shows a text file using the more command

Then it exits immediately

That's why people get kicked out!



Step 5: Exit and Download the SSH Key



Now exit from bandit25 to return to your local machine:



```bash exit ```



You should now be back on your local machine.



Step 6: Download the SSH Key to Your Local Machine



From your local machine, download the SSH key using scp:



```bash scp -P 2220 bandit25@bandit.labs.overthewire.org:bandit26.sshkey . ```



When prompted, enter the password for bandit25.



The key will be downloaded to your current directory.



Step 7: Set Proper Permissions on the Key



```bash chmod 600 bandit26.sshkey ```



This is required for SSH to accept the key.



Step 8: MAKE YOUR TERMINAL WINDOW VERY SMALL! ⭐



This is the MOST IMPORTANT step!



Before we login, make your terminal window super tiny:



Grab the corner or edge of your terminal window



Make it super small - about 3-5 lines tall



Make it look like this:



+------------------+

| [tiny window]    |

| [only a few]     |

| [lines tall]     |

+------------------+





The smaller, the better! This is the KEY to making this work!



Step 9: Login to Bandit26 from Your Local Machine



Now from your local machine with the tiny terminal, use the SSH key to login:



```bash ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220 ```



Because your terminal is tiny, you should see something like:



 _                     _ _ _   

| |                   | (_) | 



--More--(50%)





Perfect! The --More-- message means it's waiting for you! 🎉



If you don't see --More-- and get kicked out, your terminal is not small enough. Make it even SMALLER and try again!



Step 10: Press 'v' to Open the Vi Editor



While you see the --More-- prompt, press the letter v (just the letter v, no Enter needed).



This opens the Vi text editor!



Step 11: Change the Shell to Bash



Now we're in the Vi editor. Type exactly this (including the colon):



:set shell=/bin/bash



Then press Enter.



You won't see much happen, but that's okay!



Step 12: Open a Shell



Still in Vi, type this:



:shell



Then press Enter.



Success! You should now have a normal bash prompt as bandit26! 🎉



Step 13: Read the Password



Now you can read the password:



```bash cat /etc/bandit_pass/bandit26 ```



**password level 25-26:** ######################################## 

