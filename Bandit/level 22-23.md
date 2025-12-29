**Bandit Level 22 → Level 23 Write-up**

**Level Goal**



A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.



NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.



**Concepts Tested**



* Reading and analyzing shell scripts
* Understanding bash script logic
* Working with command substitution
* MD5 hashing
* Understanding how scripts generate dynamic filenames



**Solution**



Step 1: Connect to Bandit Level 22



SSH into the server using the password from the previous level:



```bash ssh bandit22@bandit.labs.overthewire.org -p 2220 ```



Step 2: Check the Cron Directory



Navigate to and examine the cron jobs:



```bash cd /etc/cron.d/ ```



```bash ls ```



```bash cat cronjob_bandit23 ```



You'll see something like:



@reboot bandit23 /usr/bin/cronjob_bandit23.sh  \&> /dev/null

* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  \&> /dev/null



This shows the script runs as bandit23 every minute.



Step 3: Read the Script



Examine what the script does:



```bash cat /usr/bin/cronjob_bandit23.sh ```



You'll see a script like:



#!/bin/bash

myname=$(whoami)

mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget



Step 4: Understand What the Script Does



Script breakdown:



1. myname=$(whoami)                                                -> Gets the username of who's running the script
2. mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)   -> Creates an MD5 hash



Copies the password to /tmp/$mytarget



When the cron job runs as bandit23, $myname becomes "bandit23".



Step 5: Replicate the Script Logic



You need to figure out what filename the script creates when run as bandit23. Run the same commands manually, substituting "bandit23" for the username:



```bash echo I am user bandit23 | md5sum | cut -d ' ' -f 1 ```



This will output an MD5 hash, something like:



8ca319486bfbbc3663ea0fbe81326349



Step 6: Read the Password File



Now read the file in /tmp with that hash as the filename:



```bash cat /tmp/8ca319486bfbbc3663ea0fbe81326349 ```





**password level 22-23:** ###################################







