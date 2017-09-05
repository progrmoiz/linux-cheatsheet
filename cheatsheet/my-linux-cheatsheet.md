## Navigation
Commands | Result
--- | ---
pwd | Print working directory
cd | change directory
ls | list directory contents

### Common `cd` usage
Shortcut | Result
--- | ---
cd | change the working directory to your home directory
cd - | change the working directory to previous working directory
cd ~user_name | change the working directory to the home directory of user_name

---

## Exploring the System
Commands | Result
--- | ---
ls | list directory contnet
file | Determine file type
less | View file contentre

### Common _`ls`_ option
Option | Long Option | Description
--- | --- | ---
-a | --all | List all files those with name that begins with a period, which are normally hidden
-A | --almost-all | Like -a option above except it does not list '.' and '..'
-d | --directory | Use this option in conjunction with `_l` option to see detail about the directory rather than its content
-F | --classify | This option will append an indicator character to the end of each listed name.
-h | --human-readable | In long format listings, display file sizes in human readable format rather than in bytes.
-l | | display results in long format
-r | --reverse | Display the result in reverse order
-S | | Sort results by file size
-t | | Sort by modification time

---

## Manipulating Files And Directories
Command | Result
--- | ---
cp | Copy files and directories
mv | Move/rename file and directories
mkdir | Create directories
rm | Remove files and directories
ln | Create hard and symlink

### Common `cp` options
Option | Description
--- | ---
-a, --archive | Copy the files and directories and all their attributes
-i, --interactive | Before overwriting an existing file, prompt the user
-r, --recursive | Recursively copy directories and their content
-u, --update | When copying files from one directory to another only copy files that are newer 
-v, --verbose | Display informative message as the copy is performed

### Common `mv` options
Option | Description
--- | ---
-i, --interactive | Before overwriting an existing file, prompt the user
-u, --update | When moving files from one directory to another only move files that are newer 
-v, --verbose | Display informative message as the move is performed

### Common `rv` Options
Option | Description
--- | ---
-i, --interactive | Before deleting an existing file, prompt the user
-r, --recursive | Recursively delete directories and their content
-f, --force | Ignore nonexistent files and do not prompt
-v, --verbose | Display informative message as the deletion is performed

### Wildcards
Wildcard | Meaning
--- | ---
\* | Matches any character
? | Matches any single character
[characters] | Matches any character that is a member of the set character
[!characters] | Matches any character that is not a member of the set character
[[:class:]] | Matches any character that is a member of the specified class

### Commonly used character class
Character Class | Meaning
--- | ---
[:alnum:] | Matches any alphanumeric character
[:alpha:] | Matches any alphabetic character
[:digit:] | Matches any numeral
[:lower:] | Matches any lowercase letter
[:upper:] | Matches any uppercase letter 

### Wildcards Example
Pattern | Matches
--- | ---
\* | All files
g* | All files beginning with 'g'
b*.txt | Any file beginning with 'b' followed by any character and ending with '.txt'
Data??? | All file beginning with 'Data' followed by exactly three character
[abc]* | Any file beginning with either 'a' or 'b' or 'c'
BACKUP.[0-9][0-9][0-9] | Any file beginning with 'BACKUP.' followed by three numerals
[[:upper:]]* | Any file beginning with an uppercase letter
[![:digit:]]* | Any file not beginning with a numeral
*[[:lower]123] | Any file ending with a lowercase letter or the numerals 1, 2, or 3

---

## Working with commands
Command | Meaning
--- | ---
type | Indicate how a command name is intepreted
which | Display which executable program will be executed
help | Get help for shell builtin
man | Display a command's manual page
apropos | Display a list of appropriate commands
info | Display a command's info entry
whatis | Display a very brief description of a command
alias | Create an alias for a command

### What are commands?
1. An executable program
2. A command built into the shell itself
3. A shell function
4. An alias

### type - Display A Command's Type 

```
[me@linuxbox ~]$ type type
type is a shell builtin
[me@linuxbox ~]$ type ls
ls is aliased to `ls --color=tty'
[me@linuxbox ~]$ type cp
cp is /bin/cp
```

### which - Display an Executable location
Sometimes there is more than one version of executable program installed on a system, to know version of program is executing which commands comes in.

```
[me@linuxbox ~]$ which ls
/bin/ls
```
### Getting a Command Documentation
#### --help - Display usage information
Many commands program support a `--help` option that display a description of the command's supported syntax and option.

#### man - Display a program's manual page
```
[me@linuxbox ~]$ man program_name
```

##### Man Page Organization
Section | Contents
1 | User commands
2 | Programming interface for kernal system calls
3 | Programming interface to the C library
4 | Special files such as device nodes and driver
5 | File formats
6 | Games and amusements such as screensaver
7 | Miscellaneous
8 | System administration commands

Sometime we need to look at specific section of man page

```
[me@linuxbox ~]$ man section program_name
```

#### apropos - Display Appropriate Commands
```
[me@linuxbox ~]$ apropos passwd
chgpasswd (8)        - update group passwords in batch mode
chpasswd (8)         - update passwords in batch mode
fgetpwent_r (3)      - get passwd file entry reentrantly
getpwent_r (3)       - get passwd file entry reentrantly
gpasswd (1)          - administer /etc/group and /etc/gshadow
grub-mkpasswd-pbkdf2 (1) - generate hashed password for GRUB
pam_localuser (8)    - require users to be listed in /etc/passwd
passwd (1)           - change user password
passwd (1ssl)        - compute password hashes
passwd (5)           - the password file
passwd2des (3)       - RFS password encryption
update-passwd (8)    - safely update /etc/passwd, /etc/shadow and /etc/group
```
Note: the man command with `-k` option perform the exact same function as `apropos`

#### whatis - Display a very brief description of a command
```
[me@linuxbox ~]$ whatis ls
ls (1)               - list directory contents
```

#### info - Display a program info entry
Alternative to man page. Info page are hyperlinked much like web page. A hyperlink can be identified by its leading asterisk and is activated by placing a cursor on it and hit enter key.

To invoke `info` type "info" followed optionally by the name of the program. Below is a table of commands used to control the reader while displaying an info page.

##### info Commands
Command | Action
? | Display command help
PgUp or Backspace | Display previous page
PgDn or Space | Display next page
n | Next - Display next node
p | Previous - Display previous node
u | Up - Display the parent node of the currently displayed node, usually a menu
Enter | Follow the hyperlink at the cursor location
q | Quit

##### README and Other Program Documentation Files
Many software package installed on your system have documentation files residing in the /usr/share/doc directory. Most of these are stored in plain text format and can  be viewed with less. Some of the files are HTML format and can be viewed in browser. We may encounter some .gz files these are compressed files and can be view with zless

##### Creating your own commands with alias
```
alias name='string'
```

```
[me@linuxbox ~]$ alias foo='cd /usr; ls; cd -'
```

```
[me@linuxbox ~]$ alias
alias l.='ls -d .* --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
```

to unalias a command
```
unalias name
```

## Redirection
Commands | Result
--- | ---
cat | Concatenate files
sort | Sort lines of text
uniq | Report or omit repeated lines
grep | Print lines matching a pattern
wc | Print newline, word and byte count for each files
head | Output the first part of file
tail | Output the last part of file
tee | Read from standard input and write to standard output and files

### Redirecting Standard Output
```
[me@linuxbox ~]$ ls -l /usr/bin > ls-output.txt
```
when you do the above way the file is overwritten means that any content in file will replace with new output of program, for appending use >> instead of >

```
[me@linuxbox ~]$ ls -l /usr/bin >> ls-output.txt
```

### Redirecting Standard Error
Standard error we must refer to its file descriptor. While we have referred to the first three of these file streams as standard input, output and error, the shell references them internally as file descriptors 0, 1 and 2, respectively

Since standard error is the same as file descriptor number 2,
we can redirect standard error with this notation:

```
[me@linuxbox ~]$ ls -l /bin/usr 2> ls-error.txt
```

### Redirecting Standard Output And Standard Error To One File
```
[me@linuxbox ~]$ ls -l /bin/usr > ls-output.txt 2>&1
```
Recent versions of bash provide a second, more streamlined method for performing this combined redirection:
```
[me@linuxbox ~]$ ls -l /bin/usr &> ls-output.txt
```

### Disposing Of Unwanted Output
Sometimes “silence is golden,” and we don't want output from a command, we just want to throw it away. This applies particularly to error and status messages. The system provides a way to do this by redirecting output to a special file called “/dev/null”. This file is a system device called a bit bucket which accepts input and does nothing with it. To suppress error messages from a command, we do this:
```
[me@linuxbox ~]$ ls -l /bin/usr 2> /dev/null
```

### cat
If cat is not given any arguments, it reads from standard input and since standard input is, by default, attached to the keyboard, it's waiting for us to type something! Try adding the following text and pressing Enter: 
```
[me@linuxbox ~]$ cat > lazy_dog.txt
The quick brown fox jumped over the lazy dog.
```

### Standard Input
Using the “<” redirection operator, we change the source of standard input from the keyboard to the file lazy_dog.txt. We see that the result is the same as passing a single filename argument. This is not particularly useful compared to passing a filename argument, but it serves to demonstrate using a file as a source of standard input. Other commands make better use of standard input, as we shall soon see.
```
[me@linuxbox ~]$ cat < lazy_dog.txt
The quick brown fox jumped over the lazy dog.
```

### Pipelines
```
command1 | command2
```

### Filter - Sort
```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | less
```

### uniq - Report Or Omit Repeated Lines
```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | uniq | less
```
if you want to see duplicate instead use `-d` option
[me@linuxbox ~]$ ls /bin /usr/bin | sort | uniq -d | less

### wc – Print Line, Word, And Byte Counts
```
[me@linuxbox ~]$ wc ls-output.txt
7902 64566 503634 ls-output.txt
```
In this case it print three number: lines, words, bytes contained in ls-output.txt. The `-l` option can be used to output only lines
```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | uniq | wc -l
2728
```

### grep - Print lines matching a pattern
grep is one of the powerful program. it use to find text pattern within files.
```
grep pattern [file...]
```
The patterns that grep can match can be very complex, you can use regular expression also here
```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | uniq | grep zip
bunzip2
bzip2
gunzip
gzip
unzip
zip
zipcloak
zipgrep
zipinfo
zipnote
zipsplit
```
There are couple of handy options for grep: `-i` which causes grep to ignore case when performing the search, `-v` which print lines that dont match the pattern

### head/tail - Print First/Last part of files
Sometime you don't want the full output from a command. You may only want the first few lines or the last few lines. The head command prints the first ten lines of a file and the tail command prints the last ten lines. By default, both commands print ten lines of text, but this can be adjusted with the “-n” option:
```
[me@linuxbox ~]$ head -n 5 ls-output.txt
total 343496
-rwxr-xr-x 1 root root 31316 2007-12-05 08:58 [
-rwxr-xr-x 1 root root 8240 2007-12-09 13:39 411toppm
-rwxr-xr-x 1 root root 111276 2007-11-26 14:27 a2p
-rwxr-xr-x 1 root root 25368 2006-10-06 20:16 a52dec
[me@linuxbox ~]$ tail -n 5 ls-output.txt
-rwxr-xr-x 1 root root 5234 2007-06-27 10:56 znew
-rwxr-xr-x 1 root root 691 2005-09-10 04:21 zonetab2pot.py
-rw-r--r-- 1 root root 930 2007-11-01 12:23 zonetab2pot.pyc
-rw-r--r-- 1 root root 930 2007-11-01 12:23 zonetab2pot.pyo
lrwxrwxrwx 1 root root 6 2016-01-31 05:22 zsoelim -> soelim
```
These can be used with pipelines as well:
```
[me@linuxbox ~]$ ls /usr/bin | tail -n 5
```

tail has an option which allows you to view files in real-time. This is useful for watching the progress of log files as they are being written. In the following example, we will
look at the messages file in /var/log (or the /var/log/syslog file if messages is missing). Superuser privileges are required to do this on some Linux distributions, since the /var/log/messages file may contain security information:
```
[me@linuxbox ~]$ tail -f /var/log/messages
Feb 8 13:40:05 twin4 dhclient: DHCPACK from 192.168.1.1
Feb 8 13:40:05 twin4 dhclient: bound to 192.168.1.4 -- renewal in
1652 seconds.
Feb 8 13:55:32 twin4 mountd[3953]: /var/NFSv4/musicbox exported to
both 192.168.1.0/24 and twin7.localdomain in
192.168.1.0/24,twin7.localdomain
...
```

### tee - Read From Stdin And Output To Stdout And Files
In keeping with our plumbing metaphor, Linux provides a command called tee which creates a “tee” fitting on our pipe. The tee program reads standard input and copies it to both standard output (allowing the data to continue down the pipeline) and to one or more files. This is useful for capturing a pipeline's contents at an intermediate stage of processing. Here we repeat one of our earlier examples, this time including tee to capture the 64 Pipelines entire directory listing to the file ls.txt before grep filters the pipeline's contents:
```
[me@linuxbox ~]$ ls /usr/bin | tee ls.txt | grep zip
bunzip2
bzip2
gunzip
gzip
unzip
zip
zipcloak
zipgrep
zipinfo
zipnote
zipsplit
```

---

Linux Is About Imagination
===

When I am asked to explain the difference between Windows and Linux, I often
use a toy analogy.
**Windows** is like a Game Boy. You go to the store and buy one all shiny new in the box. You take it home, turn it on and play with it. Pretty graphics, cute sounds. After a while though, you get tired of the game that came with it so you go back to the store and buy another one. This cycle repeats over and over. Finally, you go back to the store and say to the person behind the counter, “I want a game that does this!” only to be told that no such game exists because there is no “market demand” for it. Then you say, “But I only need to change this one thing!” The person behind the counter says you can't change it. The games are all sealed up in their cartridges. You discover that your toy is limited to the games that others have decided that you need and no more. 
**Linux**, on the other hand, is like the world's largest Erector Set. You open it up and it's just a huge collection of parts. A lot of steel struts, screws, nuts, gears, pulleys, motors, and a few suggestions on what to build. So you start to play with it. You build one of the suggestions and then another. After a while you discover that you have your own ideas of what to make. You don't ever have to go back to the store, as you already have everything you need. The Erector Set takes on the shape of your imagination. It does what you want. Your choice of toys is, of course, a personal thing, so which toy would you find more satisfying?

---

## 7 – Seeing The World As The Shell Sees It
Command | Result
--- | ---
echo | Display a line of text

### Expansion
Each time we type a command and press the enter key, bash performs several processes upon the text before it carries out our command. We have seen a couple of cases of how a simple character sequence, for example “*”, can have a lot of meaning to the shell. The process that makes this happen is called expansion. With expansion, we enter something and it is expanded into something else before the shell acts upon it. To demonstrate what we mean by this, let's take a look at the echo command. echo is a shell builtin that performs a very simple task. It prints out its text arguments on standard output:

```bash
[me@linuxbox ~]$ echo this is a test
this is a test
```
That's pretty straightforward. Any argument passed to echo gets displayed. Let's try another example:
```bash
[me@linuxbox ~]$ echo *
Desktop Documents ls-output.txt Music Pictures Public Templates
Videos
```
