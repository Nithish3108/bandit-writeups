**Bandit Level 29 → Level 30 Write-up**

**Level Goal**



The password for the next level is stored in a Git repository.

The password is not available in the production (master) branch, so you must explore other branches to find it.



**Concepts Tested**



* SSH login to Bandit levels
* Git repository usage
* Git branch enumeration
* Switching Git branches
* Reading sensitive data from non-production branches





**Solution**



Step 1: from localhost clone the repository and List Files in the Repository





After clone, list the files in the current directory:



```git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo ```

```bash ls ```





Output:



README.md





Step 2: Read the README File (Master Branch)



Display the contents of the README file:





```bash cat README.md ```





Output:



# Bandit Notes

Some notes for bandit30.


# credentials



- username: bandit30

- password: <no passwords in production!>





The password is not present in the master (production) branch.





Step 3: List All Git Branches



Check for other available branches in the repository:





```bash git branch -a ```





Output:



* (HEAD detached at origin/dev)
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev





The dev branch is likely to contain development data, including credentials.





Step 4: Switch to the Dev Branch



Checkout the development branch:





```bash git checkout remotes/origin/HEAD ```





Step 5: Read README File in Dev Branch



Read the README file again after switching branches:





```bash cat README.md ```





Output:



# Bandit Notes

Some notes for bandit30.



# credentials



- username: bandit30

- password: [password_here]







**password level 29-30:** ############################





