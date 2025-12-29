**Bandit Level 8 → Level 9 Write-up**

**Level Goal**



The password for the next level is stored in the file data.txt and is the only line of text that occurs only once.



**Concepts Tested**



* Sorting text with sort
* Finding unique lines with uniq
* Piping commands together
* Understanding how uniq works with sorted data



**Solution**



Step 1: Connect to Bandit Level 8

SSH into the server using the password from the previous level:



``` bash ssh bandit8@bandit.labs.overthewire.org -p 2220 ```





Step 2: Check the File

List and examine the file:



```bash ls ```



```bash cat data.txt ```



You'll see many lines of text, with most lines appearing multiple times.





Step 3: Find the Unique Line

To find the line that appears only once, use a combination of sort and uniq:



```bash sort data.txt | uniq -u ```





Breaking down the command:



1. sort data.txt   -> Sort all lines alphabetically (required for uniq to work properly)
2. |               -> Pipe operator (sends output of first command to second command)
3. uniq -u         -> Display only unique lines (lines that appear exactly once)




**password level 8-9:** #################################











