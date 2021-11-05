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


## Working with text files

### Understanding VI

VI an option for VIM, the standard text editor for linux. But they are very similar with each other.

It's based on two basic modes
1. Command Mode

  Will indicate basically what you'll do with the file, some examples: i, o, O, a...

2. Input Mode

  It's the mode where you effectively will input content into the text file.

### Creating text files with VI

To create a text file we can type _vi *filename*_

After that a new window will open, initially on *command mode*. Then we can select the *i* command (represent the INSERT option) amd type whatever we want on this file.

To finish insertion we can use *ESC* to return to the command mode and then apply the command *w* (always preceded by a *':'* on the command mode) to save the file with your modification.

If we type just *'o'* on the command mode, it will _open a new line_ and automatically turn on the INSERT mode for us to insert some text at a new line on the current file.

Some useful manipulations to do on VIM:

- If we select the VISUAL (*'v'*) mode on command mode we can select some text and then operate on it. You can use a *'d'* for cutting *'y'* for copying *'u'* to undo.

- For searching purposes we have basically 2 operators to use on command mode: *'/'* will search for elements ahead of the current cursor on the file and *'?'* will search for patterns preceding the current cursor.

- *'gg'* will turn back to the beggining of the file and *'SHIFT+g'* will move the cursor to the end of the current file.

- We can use a SEARCH & REPLACE operator either. For this, on _command mode_, we type *':%s/[pattern to search]/[pattern to replace]'*. To search and replace the pattern in the whole file you can append *'/g'* at the end of the sentence, indicating a global search.

To exit the file editor, we can use the command ':q'. Here we can _save and quit_ using *':wq'* and force it (the write or the exit) inserting a *'!'* at the end of the command sentence.

Obs: we can use nano editor too. Is a more intuitive editor, but have less options and not all linux versions has it available.

### Browsing text files with _more_ and _less_


The command _*more*_ will receive a file as an argument and present on the terminal just a portion of the file, but the thing here is that we can scroll down the content (and only down) to see *more* of the file.

The command _*less*_ is quite similar. It's based on VI editor, so we can use its commands on the content showed either. Different from _more_ command we have the freedom to scroll down, up, search for patterns... It's a more intuitive tool.

### Using _head_ and _tail_ to see file start and end

_*head*_ as a standard will show the first 10 lines of the text file.
_*tail*_ as a standard will show the last 10 lines of the text file.

Both commands will have the optional flag _*-n*_ to specify the number of lines to be shown (instead of 10).

A useful observation is that we can use the flag _*'-f'*_ with the _*tail*_ command to follow, for example, log files and see the most recent lines being written in it on real-time.

### Displaying file contents with _cat_ and _tac_

Both will print the content of the file indicated as an argument with the command. The difference is that tac will print it out reversed.

The thing to note here is that not all possibilities that are present with the _*cat*_ command are going to be available with _*tac*_, for example, _*-s*_ is just available together with the first one.

*'-A'* flag will also show non-printable elements

*'-b'* will print the line numbers with content, some text in it.

*'-n'* numbers empty lines as well

*'-s'* will remove *repeated* empty lines, turning the files more readable. 

### Working with _grep_

There is a lot of ways how we can use the command in question. _*grep*_ is basically a filtering utility command.

_*grep*_ can be used together with other commands, in a pipe, filtering the result dumpped by the first one. For example 'ps aux | grep _[process name]_'

Or we can look into files to check the content in it, maybe to search for some file or some content in specific. For example 'grep _[content to be searched]_ _[path to do the search]_'

It's important to remember that the standard for linux commands is to consider elements in a case-sensitive way. So when using _*grep*_ keep this in mind. The flag _*'-i'*_ indicates the command to ignore cases if that is the case.

Another important flag to be used is _*'-v'*_. This one will excludes the lines with the content indicated after it. So for example 'ps aux | grep ssh' will show us all the processes with 'ssh' pattern and, obviously, the grep command will be a process either, used with the 'ssh' content indicated on the search. To avoid this redundnacy on the result we can exclude lines that contains 'grep' in it, that for the example described will be only the process created by the _*grep*_ command. For this we use 'ps aux | grep ssh | grep -v grep'

The _*'-R'*_ flag will apply a recursive search into it.

_*'-A[number of lines]'*_ and _*'-B[number of lines]'*_ will dump the result of the _*grep*_ filtering along with a certain number of files *A*fter or *B*efore the searched expression.

Regular expressions can be used together with some Linux commands, mostly to generalize a group of names to be used as a value to specific arguments. It's always good to surround the regex by single commas: *'*.

_*grep*_ accepts filenames or content composed by this kind of expressions, this would turn the search more generalized, which sometimes is more useful.

In some cases, we'll need to use specific properties from6 regular expressions that are not supported by _*grep*_, then we can try to use _*egrep*_ that will use *extended* regular expressions and will support most of the properties from this kind of expressions.

### Using Common text processing utilities

Linux provides some text processing commands that allow us to process text to be shown on terminal command line.

- *cut:* filter output from a text file
- *sort:* sort files, often used in pipes
- *tr:* translates uppercase to lowercase
- *awk:* search for specific patterns
- *sed:* stream editor to batch-modify text files 

_*TODO:* fill out this section with some examples_

## Appendice
### Mount types

- NFS: Network File System 
## Sources
[1] - O'Reily Linux Fundamentals Video Course