**Bandit Level 18 → Level 19 Write-up**

 **Level Goal**



The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.



**Concepts Tested**



* Understanding shell initialization files (.bashrc)
* Bypassing shell configurations
* Executing commands via SSH without interactive shell
* SSH command execution



**Solution**



Execute Command Directly via SSH



When you SSH into a server, you can execute a command directly without starting an interactive shell. This bypasses the .bashrc file.



```bash ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme ```



Breaking down the command:



ssh bandit18@bandit.labs.overthewire.org -p 2220   -> SSH connection



cat readme                                         -> Command to execute remotely





Enter the password for bandit18 when prompted. The command will execute, display the password for bandit19



**password level 18-19:** ################################

