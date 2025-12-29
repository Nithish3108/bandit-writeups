**Bandit Level 11 → Level 12 Write-up**

**Level Goal**



The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions (ROT13 cipher).



**Concepts Tested**



* Understanding ROT13 cipher
* Using the tr (translate) command
* Character substitution
* Caesar cipher concepts



**Solution**



Step 1: Connect to Bandit Level 11

SSH into the server using the password from the previous level:


```bash ssh bandit11@bandit.labs.overthewire.org -p 2220 ```



Step 2: Check the File

List and view the file:



```bash ls ```

```bash cat data.txt ```



You'll see text that looks scrambled but readable, like:

Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi



Step 3: Decode Using ROT13

ROT13 rotates each letter by 13 positions in the alphabet. Use the tr command to translate characters:



```bash cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m' ```



Breaking down the command:



cat data.txt               -> Display the file contents

|                          -> Pipe to the next command

tr 'A-Za-z' 'N-ZA-Mn-za-m' -> Translate characters



'A-Za-z'                   -> Input character set (all letters)

'N-ZA-Mn-za-m'             -> Output character set (rotated by 13)







How the translation works:



A→N, B→O, C→P... M→Z, N→A, O→B... Z→M

a→n, b→o, c→p... m→z, n→a, o→b... z→m



This will output:

The password is [password_here]



**password level 11-12:** ###################################





