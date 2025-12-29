**Bandit Level 31 → Level 32 Write-up**

**Level Goal**



There is a git repository at ssh://bandit31-git@localhost/home/bandit31-git/repo via the port 2220. The password for the user bandit31-git is the same as for the user bandit31.

Clone the repository and find the password for the next level.



**Important Note** ⚠️



Use Linux or Git Bash for this level! Windows PowerShell or Command Prompt may not work correctly. If you're on Windows, use Git Bash (comes with Git for Windows).



**Concepts Tested**



* Pushing changes to a Git repository
* Working with .gitignore files
* Git add, commit, and push commands
* Understanding Git configuration (user.name and user.email)
* Bypassing .gitignore rules with force flag
* Using printf vs echo for exact text output
* Cloning repositories from your local machine





**Solution**



step 1: Clone the Repository to Your Local Machine



From your local machine (in Git Bash if on Windows):



```bash git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo ```



When it asks for password, use the same password as bandit31.



You'll see:

Cloning into 'repo'...



Step 2: Go Into the Repository Folder



```bash cd repo ```



Step 3: Read the Instructions



```bash cat README.md ```



You'll see:

This time your task is to push a file to the remote repository.





Details:

   File name: key.txt

   Content: 'May I come in?'

   Branch: master



What we need to do:



Create a file called key.txt



Put exactly this text inside: May I come in?



Upload it to Git



Step 4: Create the File (Use printf!)



Important: Use printf instead of echo to avoid extra characters:





```bash printf "May I come in?" > key.txt ```





Why printf?



echo sometimes adds extra newline characters



printf gives us exactly the text we want



The server is very strict about the exact content!





Step 5: Setup Your Git Profile



Git needs to know who you are before you can save changes:



```bash git config user.name bandit31 ```



```bash git config user.email bandit31@bandit.labs.overthewire.org ```



You can use any name and email, but these work fine!



Step 6: Check What's Blocking Us



```bash cat .gitignore ```



You'll see:



*.txt



This means Git will block all .txt files! We need to force it.



Step 7: Verify Your File Content (Optional but Recommended)



Check that your file has exactly the right content:



```bash cat -A key.txt ```



You should see:



May I come in?



No extra $ or strange characters at the end!



Step 8: Force Add the File



Use the -f flag to force Git to add the file even though it's blocked:



```bash git add -f key.txt ```



Step 9: Save Your Changes (Commit)



```bash git commit -m "Add key" ```



You'll see:



[master xxxxxxx] Add key

1 file changed, 1 insertion(+)

create mode 100644 key.txt





Step 10: Upload to the Server (Push)



```bash git push origin master ```



When it asks for password, use the same password as bandit31 again.



You'll see the password in the output! 🎉



remote: ### Attempting to validate files... ####

remote:

remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.

remote:

remote: Well done! Here is the password for the next level:

remote: [password_here]

remote:

remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.





Note: You might see an error at the end like "remote rejected" - that's normal! The important part is you got the password in the output above.





**password level 31-32:** #################################







