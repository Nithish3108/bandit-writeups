**Bandit Level 32 → Level 33 Write-up**

**Level Goal**







After logging in, you are placed inside a restricted shell that converts all input to uppercase.



The goal is to escape this uppercase shell and retrieve the password for the next level.







**Concepts Tested**





* Restricted shell behavior

* Command case sensitivity in Linux

* Environment variables

* Shell escaping techniques

* SUID binaries

* Privilege context verification







**Solution**



Step 1: Login to Bandit Level 32



```bash ssh bandit32@bandit.labs.overthewire.org -p 2220 ```



Enter the password obtained from Level 31 → 32.



Step 2: Identify the Restricted Shell



After logging in, you are greeted with:


WELCOME TO THE UPPERCASE SHELL

>>



Testing a normal command:



```bash ls ```




Output:



sh: 1: LS: not found




🔍 Observation:


All commands are converted to uppercase



Standard Linux commands fail



This confirms we are inside a restricted uppercase shell




Step 3: Analyze the Weakness



In Linux:



Commands are case-sensitive




Environment variables are expanded before case conversion





The variable $0 references the current shell.




Step 4: Escape the Uppercase Shell




Execute the following command:







```bash $0 ```




This spawns a normal shell, bypassing the uppercase restriction.







The prompt now changes to:




$




Step 5: List Files







```bash ls -la ```




Output:




-rwsr-x---  1 bandit33 bandit32 7556 May  7  2020 uppershell





🔍 Observation:




The file uppershell is owned by bandit33





It has the SUID bit set





Executing it runs with bandit33 privileges





Step 6: Confirm Current User




```bash whoami ```





Output:





bandit33




This confirms we are running commands as bandit33.





Step 7: Read the Password File





Now read the password for the next level:











```bash cat /etc/bandit_pass/bandit33 ```











**password level 32-33:** ################################



