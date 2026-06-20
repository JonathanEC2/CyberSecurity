
Linux Found2026-05-09 00:23
Tags: [[]]

# Linux Foundation


An Operating System is s collection of software that manages hardware resources and provides an environment where applications can run
A Kernel is the core of the operating system, sits between the hardware and applications
Linux Distributions are a Linux kernel plus additional software, each distribution has its own focus

## The Shell 

The shell is the default user interface to a Linux system. It is a program that accepts your commands and executes those commands

`~ ` represents the home directory

# File System & Directories

## Common Directories

**/bin** is where you find binary files and executable programs. Programs are written in human readable text and which are then compiled into binaries
**/etc** is where you find configuration files. These files control how the operating system or applications behave
**/opt** is where optional third party software is stored
**/tmp** is for temporary space, cleared at reboot
**/var** is for variable data, these are for things that change often such as log files
**/boot** files needed to boot the OS
**/root** is the home directory for the root account

## Directory Shortcuts

`.` this directory
`.. ` parent directory
`cd`  changes to previous directory

## Directory Navigation

ls -l output

- Permissions
- Number of links
- Owner name 
- Group name
- Number of bytes in the file
- Last modification
- File name

`pwd` present working directory
`cd {dir} `changes the current working directory, if you don't provide a directory to change into it will place you back into your home directory

## Creating and removing Directories

- **mkdir** created directories
- **rmdir** removes directories, only removes directories that are empty
- **rm -rf** recursively removes directories, deletes everything in a directory

some applications that are not bundled with a Linux operating system or distribution are installed in user local, and often they're installed in `user/local/{program name}`. Others will be stored in `/opt`

## Tree Command

` ls -R` list directories recursively
` tree -d` list directories only
` tree -C` colorize output

## Directory Tips

- <span style="color:rgb(255, 0, 0)"> DO NOT USE SPACES IN DIRECTORY NAMES</span>
- use quotes around directories that have spaces

# Command Line Fundamentals

`cat`  displays contents of files
`clear` clears screen
`man {command}` displays the online manual for the command'
`exit`  logs out of current session

## MAN page navigation 

- `g` moves to top of the page
- `(Shift + G)` moves to the bottom of the page
- `q` quit
- `man -k {search term}`  search through man pages

## Get Help

--help or -h for help

## Environment Variables

Storage location that has a name and a value
Typically uppercase
## $PATH

- PATH controls the command search path
- PATH contains a list of directories
- `which` command tells you the full path to the command that you're executing
- PATH environment variable gives you an idea of where commands are located on a Linux system
- If you have an idea of something you want to do but not sure how to do it, you could start by looking in PATH
## Executing Commands

`$PATH` determines command search path
You can execute a command not in path
`./{command}` executes the command in this directory


# Files and File Operation

## Viewing Files

**cat {file}** displays content of file
**more {file}** Browse through a text file
**less {file}** more features than more
**head {file}** Outputs the beginning portion of file
**tail {file}** outputs the ending portion of file

tail -f {file} follows the file and displays data as it is being written

## File Management

- `rm` removes files
- `cp {source file} {destination file}` copies file
	- can copy files into a directory, will only work on directories if you use the -r modifier
- `mv` moves or renames
- `sort` sorts text in file
- `uniq`- searches for unique lines; For unique to filter for unique lines, the lines need to be sorted
- `tar c|x|t f tarfile {directory}` bundles a group of files or directories together in an archive

## Archiving and Compression

**gzip** compress files
**gunzip** uncompress files
**gzcat** concatenates compressed files
**du** disk usage

## Comparing Files 

**diff {file1} {file2}** - compares two files
	c changed
	d deleted
	a addition
**sdiff {file1} {file2}** -  side by side comparison
**vimdiff {file1} {file2}** - highlights differences in vim
	Ctrl-w w switch windows

## Hidden Files

Hidden files start with a period
-a option shows hidden files
-F reveals file  type
	/ is directory
	@ is a link
	* is executable

## Symbolic Link

points to the actual file or directory and uses the link as if it were the file

# Permissions and Access Control

| Symbol | Type          |
| ------ | ------------- |
| \-     | Regular file  |
| d      | Directory     |
| l      | symbolic link |

## Files vs Directories

| Permission | File                        | Directory                                              |
| ---------- | --------------------------- | ------------------------------------------------------ |
| Read       | Allows file to be read      | Allows file names in the directory to be read          |
| Write      | Allows files to be modified | Allows entries to be modified within the directory     |
| Execute    | Allows execution of a file  | Allows access to the contents and metadata for entries |

## Categories

| Symbol | Category |
| ------ | -------- |
| u      | User     |
| g      | Group    |
| o      | Other    |
| a      | All      |

## Groups

- Every user is in at least one group 
- Users can belong in many groups
- use `group` command to see what group someone is in

- When you create a file, its group is set to your primary group
- The `chgrp` command changes the group

## Secret Decoder Ring

| Type | User | Group | Other |
| ---- | ---- | ----- | ----- |
| -    | rw-  | r--   | r--   |

## Changing Permissions

### Symbolic Notation

- **chmod** change mode comman
- **ugoa** user category user, group, other, all
- **+-=** add subtract or set permissions
- **rwx** Read Write Execute

You can separate permissions for different categories using comma:
`chmod u+rwx,g-x sales.data`

not specifying any permissions removes all permissions

### Numeric (Octal) Notation

|                      | r   | w   | x   |
| -------------------- | --- | --- | --- |
| Value for off        | 0   | 0   | 0   |
| Binary Value for on  | 1   | 1   | 1   |
| Base 10 Value for on | 4   | 2   | 1   |

<span style="color:rgb(255, 0, 0)">Avoid 777 and 666 permission modes</span>

### Directory Permissions Revisited

Permissions on a directory can affect the files in the directory
If the file permissions look correct, start checking directory permissions working your way up to the root

### File Creation Masks

File creation masks determine default permissions on a file usually set by an admin. If not masks were set **directories are set to 777 and files are set to 666**
`umask` command overwrites can overwrite this:
`umask {-S} {mode} `

This work opposite of chmod so using 7 would mean no permissions

chmod turns on, adds, and gives permissions
umask turns off, subtracts, and takes away permissions

When using umask, subtract the umask from the default values to determine what the output would be

### Special Modes

setuid, setgid, and sticky.
special modes are declared by prepending a character to the octal mode that you normally use with umask or chmod.

`touch` creates a file if it doesn't exist or updates the timestamp of a file

# Search, Filtering, and Data Processing

`find {path} {expression} `recursively finds files in path that match the expression. If no arguments are supplied, it finds all files in the current directory

`find . -exec file {}\; `will find everything in the current directory and will execute the file command against all the search results that are returned

`locate {pattern}` list files that match a pattern
Faster than the find command
Queries an index
Results are not in real time

## Searching in Files and Using Pipes

- `grep {pattern} {file}` - displays lines matching a pattern
- `file {file}` - displays the file type
- `strings` - looks at textual data in a binary file
- `|`  pipe takes the standard output from the preceding command and passes it as the standard input in the following command. 
- `cut` - cuts out selected portion of a file
- `tr` - translate characters 
- `column` - table format

# Wildcards and Pattern Matching

A wildcard is a character or string used for pattern matching
Globbing is the act of expanding a wildcard into the list of matching files and directories

\* matches zero or more characters
? matches exactly one character, each question mark represents a single character

## Character Class

\[] - Matches any of the characters included between the bracket. Matches exactly one character
\[!] - matches any characters not included between the brackets
\[a-g] - match all characters through the range
\ - escape character if you want to match a wildcard character, try to avoid naming files with wildcard characters in them

### Named Classes

# Input, Output, and Redirection

0 - Standard Input
1 - Standard Output
2 - Standard Error

\> redirects standard output to a file; Overwrites existing content
\>> Redirects standard output to a file; appends to any existing file content
\< Redirects input from a file to a command

**Whenever we use redirection or piping, the data is sent anonymously**
If you want to use a file descriptor instead of a filename, use &
If you want to ignore output, you can send it to /dev/null


`ls files.txt not-here > out.both 2>&1` would send both standard output and standard error to the same file 

# Editing, Customization, and Remote Access

## Nano 
nano is a simple editor and easy to learn
Not as advances as vi or emacs

## VI 

Advanced and powerful features
Harder to learn than nano, requires time investment

### VI Editor 

vi {file} edit file
vim {file} same as vi, but no features
view {file} starts vim  in read-only mode

### VI Modes

Command mode - allows you to navigate the file (Esc)
Insert mode -  use i I a A
Line mode - use :

`vimtutor`

## Emacs

Powerful editor
VI or Emacs are both good, depends on preference

## Transferring and Copying Files over the Network

scp (secure copy) - `scp {source} {destination}:` append colon to specify path
sftp (ssh file transfer protocol) `sftp {host}` starts a secure file transfer session with host

## Customizing the Shell Prompt

- Bash, ksh, and sh use **$PS1**.
	- `PS1="<\t \u@\h \w>\$"`
- Csh, tcsh, and zsh use **$prompt**.
- To persist changes, set the environment variable in your dot files.

## Shell Aliases

Aliases are used for long commands or commands you type often
	`alias {name} = {value} `
Can be used to fix common typos
`unalias` to remove alias
To persist changes, set the environment variable in your dot files.

# Environment Variables

Storage location that has a Name/Value pair. It can change how an application behaves
Environment variable are uppercase by convention

`printenv` to view environment variables
Syntax for creating Environment Variables `export VAR='value'`
	`export EDITOR='vi'`
`unset` removes environment variables

# Processes and Job Control

- `ps` display process status
- `pstree` process tree
- `top` interactive process viewer

## Background and Foreground Processes

Place `&` at the end of a command to send it to the background
Ctrl-C kills the foreground process
Ctrl-Z suspends the foreground process

- `bg {%num} `backgrounds a suspended process
- `bfg {%num} ` foregrounds a background process
- `kill` kills a process by job number or PID
- `jobs {%num} ` lists jobs

The current job is considered to be the last job that was suspended while it was in the foreground or the last job started in the background 

A hard to kill process would use SIGKILL or -9
## Cron

`cron` - a time based job scheduling service
`crontab` - a program to create, read, update, and delete your job schedules

![[attachments/Pasted image 20260508230548.png]]

\*/15 * * * * would run a command every 15 minutes
0-4 * * * * would run command for first 5 minutes of the hour

## Switching Users and Running Commands as Others

`su` change user or become superuser
	`-` used to provide an environment similar to what the user would expect had the user logged in directly
	`-c `command specifies a command to be executed; must surround with quotes if command is longer than one word
`whoami` shows what user you are

`sudo` executes a command as another user, typically the super user. You don't need to know the password of the other user, you are prompted for your password

## Sudoers Format

`user host=(users) [NOPASSWD:]commands`

### References