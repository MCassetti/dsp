# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

> > __Command Cheat Sheet__ 

* show current working directory path - ls
* creating a directory: mkdir
* deleting a directory: rm -rf
* creating a file using `touch` command: touch file
* deleting a file:  rm -f
* renaming a file:  mv file1 file2
* listing hidden files: ls -a
* copying a file from one directory to another: cp -r dir1 dir2
* find a file containing name foo starting in current dir: find . -name foo
* concatenate two files and write to new file: cat file1 file2 > newfile
---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`  

> > __List Commands__

* `ls`: Directory Listing  
* `ls -a`: Directory listing with hidden files that start with '.' 
* `ls -l`: Directory listing long format and permissions  
* `ls -lh`: Directory listing long format and human readable  
* `ls -lah`: Directory listing long format human readable including hidden files   
* `ls -t`: Directory listing sorted by time and date  
* `ls -Glp`: Direcotry listing colorized, long formatting, and slash after each directory
---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

> > __Favorite List Commands__

* `ls -m`: Comma separated list
* `ls -d */`: Displays directories within current directly, only
* `ls -1`: Displays each entry on a separate line
* `ls -lt`: Long format and newest first
* `ls -R`: Also dispays sub directories

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

> > __Xargs Example__
xargs is used to convert the standard input into arguments

* find . -name foo | xargs vim 

 
