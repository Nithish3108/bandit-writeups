**Bandit Level 27 → Level 28 Write-up**

**Level Goal**



There is a git repository at

ssh://bandit27-git@localhost/home/bandit27-git/repo

accessible via port 2220.



The password for the user bandit27-git is the same as the password for bandit27.



Clone the repository and find the password for bandit28.





**Concept Tested**



* Accessing a Git repository over SSH
* Using non-default SSH ports
* Understanding that credentials can be stored inside Git repositories
* Basic usage of git clone in restricted environments
* 



**Solution** 






Step 1: From the localhost Clone the Git Repository (Specify Port)



Clone the repository using SSH on port 2220:





```bash git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo ```





When prompted, enter the password of bandit27.





Step 2: Enter the Repository Directory



```bash cd repo ```



Step 3: Check What Files Are Available



```bash ls ```





You will see:



README



Step 4: Read the README File



```bash cat README ```





**password level 27-28:** #################################







