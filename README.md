# Intro-to-Linux-Shell-Scripting  
A shell script is simply a plain text file that contains a series of commands and shell statements when a shell script is executed ,it, in turn, executes the commands listed in the script that starts at the very top and executes the commands on each line one line at a time until the end of the file. Executing a shell script produces the exact same result as you typing in each line directly into the terminal. This means any work you can do on the command line can be automated by a shell script.    
## Text-Editor   
We need a text editor to edit and execute the shell script. If you have already installed your favorite text editor good to go! if not, then either you can install gvim, gedit or any other text editor you want. Else, you can start with `vim` or `nano` text editor. some distro comes with nano inbuilt while in some machine, we need to install it.
To install the nano text editor, execute the following command in the terminal.    

- For RedHat based system,    
`sudo yum install -y nano`     
- For Debian based system,     
`sudo apt-get install -y nano`       

In this repo, we will be using `nano` text editor to write and execute our shell script.   
- At first we open a file in nano text editor. To do so, give-   
`nano day1.sh`   
- `.sh` is the extension for the script file. However, unlike the other file formats extension is not necessary. Rather the permission to execute the file is of the top most priority. To check the read, write & executable status of the file give, `ls -l` in the terminal.   
- This should return,   
`-rw-r--r-- 1 dell dell 0 Apr 16 15:14 day1.sh`    
- Let's breakdown the above-     
`-` denotes that it's a text file.       
`d`  denotes that it's a directory.    
`r` read permission    
`w` write permission      
   
- So, we can see that our file `day1.sh` doesn't have execute permission. To make the file executable give,     
```
chmod +x day1.sh    
or
chmod +xr day1.sh
```      
- Where, `chmod` stands for change of mode and `+x` is the file execute permission. after this, again run `ls -l` on the terminal.   
- Now the output comes as-   
```
-rwxr-xr-x 1 dell dell 0 Apr 16 15:17 day1.sh    
where, x is executable permission
```     

NOTE- In the command, `-rwxr-xr-x`   
1. `-` denotes its a text file.       
2. First three `rwx` denotes permission given to the owner of the file.      
3. Next three `r-x` denotes permission given to the group of the file.        
4. Last three `r-x` denotes permisison given to everyone else in the system.
      
To execute the file, you need to have read and execute permisison of that file.         
- Since now we have execute permisison, it's time to execute the file. But, before that, let's add some content in the file `day1.sh` so that we can see them executing. To do so, open the file through `nano day1.sh` command and add the following to it.          
```
#!/bin/bash
echo "You don't need to be great to start something but, you need to start to be great.
```
            
- Then, `ctrl+o` to save and `enter` to confirm the file name and exit. Further, give the `./day1.sh` to execute the file.     
- After executing, the output shall be following-          
`You don't need to be great to start something but, you need to start to be great.`                  
- Have you noticed, we wrote `#!/bin/bash` in the top line in our file `day1.sh`. What does that mean???             
- The `#!` means `shebang` It determines what path the program will be executing in the file.     
- The `echo` however is a builtin command to print the content in the file.                                
- How to know type of the command we are giving??? just give the below command on the terminal.               
`type <command>`                           
- The command & output will be following-            
```tcl
~$ type echo
echo is a shell builtin
```         

## Working with Variable(s)-                                   
Lets try to add some variables to our script and execute it.                       
- Let the variable be `SKILL`.                                  
```
#!/bin/bash
SKILL= "Shell Scripting"
echo "I am best at ${SKILL}. and trying to learn more about ${SKILL}."
```                            
- The output will come as-                              
`I am best at Shell Scripting. and trying to learn more about Shell Scripting.`                

So, what did we notice?? SKILL was our variable. and "Shell Scripting" was the value assigned to the SKILL variable.    
In the second line, to call the `SKILL` variable, we used `${}`; inside the braces, we call our variable.                  

Rules for the variable declaration-                            
1. Variable names can contain Letters, Digits & Underscore.                      
2. However the variable name can only start with Letters and undercore.                          
3. For convention, try to write the variables in Uppercase only. (It is not an Rule and you can also write in Lowercase)                             
Some Valid Examples are-                      
` SKILL  Skill  _Skill  skill  SkILL`                  
Invalid Variable Examples-                      
`0Skill 1_SKILL -SKILL @skill S@kill`                   
NOTE-

## Writing Long and Complicated Scripts-
We learned that it's a good practice to start your scripts with a comment or a letter that describes the goal of the script. Let's try an example-   
```
#!/bin/bash

#this script displays information about the system on which it is executed.

#tell the user the script is starting.
echo "Starting the sysinfo script."

#Display the hostname of the system.
hostname

#Display the current date and time when this information is collected.
date

#Display the kernel release follwed by the architecture
uname -r
uname -m

#Display the disk usage in a human reading format
df -h

#Ending the script
echo "Stopping the code."
```
## Decision making on Shell-   
When you start automating your work with shell scripts you have to put your good decision making abilities into your scripts.    
- One way to do this is by using IF statements in real life.
- Let's create a script that displays if the user running that script is using the root account or root.
```
#!/bin/bash

#determine if the user executing this script is the user or not.

#Display the UID
echo "Your UID is ${UID}"

#Display if the user is the root or not.
if [[ "${UID}" -eq 0 ]]
then
	echo "You are root."
else
	echo "You are not root"
fi
```
Let's modify the code with a real example.    
- For example if you write a shell script that install software you want to make sure the person executing the script is using root privileges because root privileges are required to install software.
- So let's edit our script again and change it slightly such that it could fit this example.
```
#!/bin/bash

#determine if the user executing this script is the user or not.

#Display the UID
echo "Your UID is ${UID}"

#Display if the user is the root or not.
if [[ "${UID}" -eq 0 ]]
then
	echo "installing software"
	#The commands to install the software.
else
	echo "You do not have the permission to install the software"
fi
```












