**Bandit Level 12 → Level 13 Write-up**

**Level Goal**



The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the man pages!).



**Concepts Tested**



* Understanding hexdumps and xxd

* Working with compressed files (gzip, bzip2, tar)

* Identifying file types

* Multiple compression/archive layers

* Working in /tmp directory



**Solution**



Step 1: Connect to Bandit Level 12

SSH into the server using the password from the previous level:



```bash ssh bandit12@bandit.labs.overthewire.org -p 2220 ```



Step 2: Create a Working Directory



Use mktemp -d to create a secure temporary directory:



```bash mktemp -d ```



This will output something like /tmp/tmp.Ykgk3V5Oke



Step 3: Copy the Data File



Copy data.txt to your working directory:



```bash cp data.txt /tmp/tmp.Ykgk3V5Oke/data.txt ```



```bash cd /tmp/tmp.Ykgk3V5Oke ```



Step 4: Check the File



Verify the file is a hexdump:



```bash file data.txt ```

```bash cat data.txt ```



You'll see it's ASCII text containing hexadecimal data like:

00000000: 1f8b 0808 2e17 ee68 0203 6461 7461 322e



Step 5: Reverse the Hexdump



Convert the hexdump back to binary:



```bash xxd -r data.txt data1 ```



Step 6: Decompress Layer 1 - Gzip



Check the file type and decompress:



```bash file data1 ```



\# Output: gzip compressed data, was "data2.bin"...



```bash mv data1 data.gz ```



```bash  gzip -d data.gz ```



Step 7: Decompress Layer 2 - Bzip2



Check and decompress again:



```bash file data ```



\# Output: bzip2 compressed data, block size = 900k



```bash mv data data.bz2 ```



```bash  bzip2 -d data.bz2 ```



Step 8: Decompress Layer 3 - Gzip Again



Check and decompress:



```bash file data ```



\# Output: gzip compressed data, was "data4.bin"...



```bash mv data data.gz ```



```bash  gzip -d data.gz ```



Step 9: Extract Layer 4 - Tar Archive



Check and extract:



```bash file data ```



\# Output: POSIX tar archive (GNU)



```bash tar -xf data ```



```bash ls ```



\# You'll see data5.bin



Step 10: Extract Layer 5 - Tar Archive Again



Check and extract data5.bin:



```bash file data5.bin ```



\# Output: POSIX tar archive (GNU)



```bash tar -xf data5.bin ```



```bash  ls ```



\# You'll see data6.bin



Step 11: Decompress Layer 6 - Bzip2 Again



Check and decompress:



```bash file data6.bin ```



\# Output: bzip2 compressed data, block size = 900k



```bash mv data6.bin data6.bin.bz2 ```



```bash  bzip2 -d data6.bin.bz2 ```



Step 12: Extract Layer 7 - Tar Archive



Check and extract:



```bash file data6.bin ```



\# Output: POSIX tar archive (GNU)



```bash tar -xf data6.bin ```



```bash  ls ```



\# You'll see data8.bin



Step 13: Decompress Layer 8 - Gzip Final



Check and decompress:



```bash file data8.bin ```



\# Output: gzip compressed data, was "data9.bin"...



```bash mv data8.bin data8.bin.gz ```



```bash  gzip -d data8.bin.gz ```



Step 14: Read the Final File



Check the file type and read it:



```bash file data8.bin ```



\# Output: ASCII text



```bash cat data8.bin ```







**password level 12-13:** ###############################







