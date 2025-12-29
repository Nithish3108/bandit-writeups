**Bandit Level 28 → Level 29 Write-up**

**Level Goal**



The password for the next level is stored in a Git repository.

You need to explore the commit history to find sensitive information that was removed in a later commit.



**Concepts Tested**



* Git repository navigation
* Reading files in a repository
* Understanding Git commit history
* Using git log
* Inspecting commits with git show
* Identifying information leaks in previous commits





**Solution**



Step 1: List Repository Files



From localhost cloning the repository, list the files:



```bash git clone ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo ```   

```bash cd repo ```

```bash ls ```





Output:



README.md





Step 2: Read the README File



View the contents of the README file:





```bash cat README.md ```





Output:



# Bandit Notes

Some notes for level29 of bandit.



# credentials



- username: bandit29

- password: xxxxxxxxxx





The password is hidden, so we need to check the Git history.





Step 3: View Commit History



List all commits in the repository:





```bash git log ```





Output:



commit b5ed4b5a3499533c2611217c8780e8ead48609f6

   fix info leak



commit 8b7c651b37ce7a94633b7b7b7c980ded19a16e4f

   add missing data



commit 6d8e5e607602b597ade7504a550a29ba03f2cca0

   initial commit of README.md





The message "fix info leak" suggests that sensitive data was removed.





Step 4: Inspect the Latest Commit



View the changes made in the commit that fixed the information leak:





```bash git show b5ed4b5a3499533c2611217c8780e8ead48609f6 ```





Step 5: Identify the Leaked Password



From the commit diff:





- password: [password_here]

+ password: xxxxxxxxxx





The password was visible in an earlier version and later hidden.





**password level 28-29:** ##########################







