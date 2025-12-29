**Bandit Level 21 → Level 22 Write-up**

**Level Goal**



A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.



**Concepts Tested**



* Understanding cron and scheduled tasks
* Reading cron configuration files
* Following script execution paths
* Linux task scheduling
* Reading and analyzing shell scripts



**Solution**



Step 1: Connect to Bandit Level 21



SSH into the server using the password from the previous level:



```bash ssh bandit21@bandit.labs.overthewire.org -p 2220 ```



Step 2: Navigate to the Cron Directory



Check the cron configuration directory:



```bash cd /etc/cron.d/ ```



```bash ls ```



You'll see multiple cron job files, including one for bandit22.



Step 3: Examine the Cron Job



Read the cron job configuration for bandit22:



```bash cat /etc/cron.d/cronjob\_bandit22 ```



You'll see something like:



@reboot bandit22 /usr/bin/cronjob_bandit22.sh \&> /dev/null

* * * * * bandit22 /usr/bin/cronjob_bandit22.sh \&> /dev/null



This shows:



The job runs as user bandit22



It executes /usr/bin/cronjob_bandit22.sh

* * * * * means it runs every minute

\&> /dev/null redirects all output to null (discards it)



Step 4: Read the Script



Examine what the script does:



```bash cat /usr/bin/cronjob_bandit22.sh ```



You'll see a script like:



bash#!/bin/bash

chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv



This script:



Sets permissions (644) on a file in /tmp

Copies bandit22's password to that temp file



Step 5: Read the Password File



Since the script makes the file readable, you can access it:



```bash cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv ```





**password level 21-22:** ######################################





