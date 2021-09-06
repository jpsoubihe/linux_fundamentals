# Linux learning

In this series we intend to document all our findings along some web courses and bibliography through the web.
It's important to mention that we're considering some previous knowledge, so some basic stuff could not be found in the following text.

## Introduction

## Using Essential Tools
### Seven Essential Linux Command Line Tools

#### whoami
- Show your current username in a Linux Terminal.
- The '--version' option give us some information about the licenses from GNU.
#### hostname 
- Show the hostname of your machine. It has a lot of options that we could set to list some other information related to it. 
- With the _less_ command after a pipe (|) we set the respective output to be shown in parts, accordingly to the size of your terminal screen.
- The option _--all-ip-addresses_ lists all IPs being used by the host.
#### date
- Show the current date. It accepts a lot of options to set the date format and related information to be shown.
#### passwd
- Command related to password operations. If displayed solely it will request a new password to change the current one for the user in the system.
- We can specify usernames as sudo to set passwords for those users.
#### touch 
- This command is mostly used to check if the current user has write permissions in some place at the system. With it we can specify a file to be created (empty). 
#### last 
- List the last logins on the system.

### Getting Help with man
With the _man_ command (an abbreviation for _manual page_) we can check a more detailed documentation regarding the native command in question. 
It is divided into sections with each of them we'll handle a specific subject on the command.
Item between [brackets] are optional.
if you see {a | b} it indicates that you must choose between option a or b.
This pages often have some examples in the end, to allow to user better comprehension.
You can use *\sometext* to search for _sometext_  along the man page or *q* to leave it.
The section represented on the command specifies the users that can execute the command. For example, section 1 commands are available for common users and section 8 commands are available only to root users. (in the man man page we can see a description for each of the sections)

 - What to do when we don't know wich command to use?
  
  The _man_ command within the *-k* option and *user* specification can list all the commands available, together with a description for each one of them.
  We can use grep to help us filter the commands by some common property, like section or description.

### Using Other Systems for Getting Help
For help in the execution of commands we can use

*man* is the primary source

*pinfo* shows usage information

*<command\>* --help provides short usage overview

*/usr/share/doc* will have several refrences to documentation for applications installed in the system

## Essential File Management Tools
### Understanding the Linux File System Hierarchy
- Linux filesystem works based on a hierarchy...
- '/' is the parent directory, the root directory, the starting point for the filesystem.
- The root directory (and others) will have sub-directories. Each of them should be related to some context, like 'bin' for binary files, and 'usr', for user related files
- _mount_ sets a specific partition, a determined segment of memory to some sub-directory. For this we have to mount the sub-dir to other disk. We can mount directories through the network too, using a NFS for example.
- Directories
  - /boot: has boot files and linux kernel
  - /etc: configuration files directory
  - /dev: the name dev comes from devices. It stores the hard disk reference (sda) and its partitions (sda1,sda2,...)
  - /home: personal environment for users
  - /opt: applications like databases
  - /proc: process files directory. It has files cpuinfo and meminfo that monitors cpu and memory usage
  - /tmp: temporary files directory
  - /var: have a deep variety of files. The most used of them is the ones stored in the /log subdirectory that stores log files from the system
   
### Using Wildcards

- Allow us to refer to files in a flexible way
- '*' means all
- '?' one single character
- '[]' comprehend variable ranges
- It's similar with regex declaration. We can use combinations of wildcards to filter the result shown by *ls*
- It's important to say too that ls together with wildcards will output just the correspondent directories. If you want to get the files in the directory, along with the directories, you can use the flag _-d_ after command

### Understanding Hard and Symbolic Links
- Links are basically shortcuts from the system
- On Linux we have two types of them
    
    1 - Hard Links
    2 - Symbolic Links (soft)

- inode: an inode is the group of all administrative data from a file. Then, every file have a respective inode.
- To be more comprehensive to humans, Linux allow us to give an inode reference one or more *names*.
- If a name refers directly to an inode, we say that the name has a *hard link* to it.
- If a name is referring to other name, e.g. a reference pointing to other reference, we name it as *symbolic link*.
- Hard Links limitations:
  - no cross device: hard links must be on same storage device
  - no hard links to directories (in this case we only use symbolic ones)
- To create links we can use the command *ln* and point the inode to be referenced followed by its names (references).
- The flag _-s_ following ln command will create soft links.
Tip: if you want to create a symbolic link, refer it to a file using its absolute path, to prevent that if the file is moved the link do not break.

### Finding Files with _find_

The _find_ command searches for files that has components similar with what is being searched, and were specified by the user
- "-name" argument receives a name to be searched in filename's.
  - 'find \ -name "hosts"' searches for files with the name "hosts", starting in the root directory. Could be a name that contains the word "hosts" in it
- "-user" argument search files belonging to user specified
  - 'find \ -user amy'
- "-exec" argument will specify an action to be executed with the files found. We can use multiple execs in a find command since we separate them by a '\;'.

For further options take a look at man page for _find_ command or type 'find --help' on your terminal.

### Archiving files with tar
TAR files basic use is to compress, extract or list files
- tar -cvf my_archive.tar /home (compress your home directory into the tar file specified)
- tar -xvf my_archive.tar (extracts my_archive.tar to the current directory. We can use -C to redirect the output to other directory)
- tar -tvf (show the contents of an archive)
- the size of the compressed files will vary accordingly to the compression engine choosed.


## Appendice
### Mount types

- NFS: Network File System 
## Sources
[1] - O'Reily Linux Fundamentals Video Course