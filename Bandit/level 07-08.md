**Bandit Level 7 → Level 8 Write-up**

**Level Goal**



The password for the next level is stored in the file data.txt next to the word millionth.



**Concepts Tested**



* Searching text within files using grep
* Understanding pattern matching
* Working with large text files
* Piping commands together



**Solution**



Step 1: Connect to Bandit Level 7

SSH into the server using the password from the previous level:



```bash ssh bandit7@bandit.labs.overthewire.org -p 2220 ```





Step 2: Check the File

List the files to confirm data.txt exists:



```bash ls ```



You'll see data.txt. If you try to view it with cat data.txt, you'll see it's a very large file with many lines.



Step 3: Search for the Word "millionth"

Use grep to search for the specific line containing "millionth":


```bash grep millionth data.txt ```


This will output something like:

millionth       [password_here]





**password level 7-8:** #################################











