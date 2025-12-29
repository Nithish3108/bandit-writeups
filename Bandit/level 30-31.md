**Bandit Level 30 → Level 31 Write-up**

**Level Goal**



There is a git repository at ssh://bandit30-git@localhost/home/bandit30-git/repo via the port 2220. The password for the user bandit30-git is the same as for the user bandit30.

Clone the repository and find the password for the next level.





**Concept Tested**



* Working with Git repositories
* Understanding Git tags
* Exploring Git references
* Finding hidden information in Git







**Solution**




Step 1: From localhost Clone the Git Repository



```bash git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo ```



When prompted for password, use the same password as bandit30.



Step 2: Navigate to the Repository



```bash cd repo ```



```bash ls ```



You'll see:



README.md



Step 3: Check the README



```bash cat README.md ```



You'll see:



just an epmty file... muahaha



Hmm, not helpful! 😕



Step 4: Check Git Log





```bash git log ```



You'll see only one commit with no useful information.



Step 5: Check for Branches



```bash git branch -a ```



Only shows the master branch. No hidden branches here.



Step 6: Check for Tags



Let's check if there are any Git tags:



```bash git tag ```



You'll see:



secret



A tag called "secret"! 🎯



Step 7: Show the Tag Content



View what the "secret" tag points to:



```bash git show secret ```





**password level 30-31:** ############################







