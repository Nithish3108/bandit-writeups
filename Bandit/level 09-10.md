**Bandit Level 9 → Level 10 Write-up**

**Level Goal**



The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several '=' characters.



**Concepts Tested**



* Extracting strings from binary files using strings
* Filtering output with grep
* Working with binary/non-text data
* Combining multiple commands with pipes
 



**Solution**



Step 1: Connect to Bandit Level 9

SSH into the server using the password from the previous level:



```bash ssh bandit9@bandit.labs.overthewire.org -p 2220 ```





Step 2: Check the File

List the files:



```bash ls ```



You'll see data.txt. If you try to view it with cat data.txt, you'll see it contains mostly binary/non-readable data.



Step 3: Extract Human-Readable Strings

Use the strings command to extract readable text from the binary file, then search for lines with multiple '=' characters:



```bash strings data.txt | grep "=" ```



Breaking down the command:



strings data.txt  -> Extract all printable character sequences from the file

|                 -> Pipe the output to the next command

grep "="          -> Filter for lines containing at least two consecutive '=' characters





You'll see output like:

========== the

========== password

========== is

========== [password_here]



The password is on the line with the most '=' characters or clearly indicated as the password.





**password level 9-10:** ##################################









