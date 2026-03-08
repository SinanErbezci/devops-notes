### The Shell Prompt
```bash
# username@hostname:/current_directory $
pete@icebox:/home/pete $
```
### Directory Tree
```bash
/ # root directory
|-- bin
|   |-- file1
|   |-- file2
|-- etc
|   |-- file3
|   `-- directory1
|       |-- file4
|       `-- file5
|-- home
|-- var
```

#### Any path that begins with / is an absolute path.
### pwd
```bash
# Print working directory
pwd
```

### cd
```bash
# Change to previous directory
cd -
```

### ls
#### In linux (.) files are hidden.
```bash
# Also show hidden files
ls -a
```

```bash
# Detailed list (long).
# file permissions, number of links, owner_name, owner group, file size, timestamp of last modification, name
ls -l
```

```bash
# Reverse order
ls -r
```

### touch
#### If you use touch on an existing file, it will update its timestamps to the current time.

```bash
# You can match timestamp with another file
touch -r file1 file2
```

```bash
# Modify exact time
touch -d "2023-01-01 12:30:00" mysuperduperfile
```

### file
#### In Linux, filenames aren't required to represent the contents of the file. You can create a file called funny.gif that isn't actually a GIF.

```bash
# Shows the description of the file contents
file text.txt
```

### cat
```bash
# Display contents of the object. cat -> concatenate
cat text.txt
```

```bash
# Display multiple files
cat text1.txt text2.txt
```

```bash
# Write text into file from the terminal
# Control + D on new line and save
# Options. -n (print line numbers). -b (only non-empty lines)
cat > text1.txt
```

```bash
# Display multiple files
cat text1.txt text2.txt
```

### less
#### View text files page by page.
Navigation and Controls:
* q -> exit
* PageUp, PageDown, Up and down to navigate 
* g -> beginning of the file
* G -> end of the file
* h -> help

You can search text. Enter "/"
* /search_term -> looks for search_term
* /?search_term -> search backwards
* n -> jumps to next occurence
* N -> previous occuruence

### history
History of commands you've entered.
* !! -> run the previous command.
* Ctrl + R -> reverse search through history
* history -c ->clear history
* history -w -> save history to ~/.bash_history

### cp
Using wildcards for bulk copying:
- "*" -> matches any sequences
- "?" -> matches single char
- "[]" -> matches those chars

```bash
# copy directories (recursively)
cp -r Pumpkin /home/pete/Pictures
```

```bash
# when there's a overwrite, it prompts for confirmation
cp -i 
```

```bash
# force overwrite
cp -f 
```

```bash
# preserve metadata(timestamp)
cp -p
```

### mv
```bash
# Renaming file or directories
mv sinan.txt ahmet.txt 
```

#### It also moves files and directories like cp command.

### mkdir
```bash
# create nested directories
mkdir -p books/series/harrypotter
```

### find
```bash
# find [path] [expression(can use wildcards)]
find /home -name sinan.txt
# search by type
find /home -type d -name sinan.txt
```

### whatis
```bash
# one line description
whatis cat
```

### alias
Rather than typing long commands create a shortcut with "alias"
```bash
alias ll='ls -la'
```

### Making alias permanent
You should save it in ~/.bashrc (bash config file)

open it with nano ~/.bashrc

close the terminal and reload it with "source"

```bash
# removing alias
unalias ll
```

### Understanding stdout(Standart out)
By default, many commands gives output to stdout which is your terminal screen.

You can redirect this by using ">". takes the data from stdout to destination.

```bash
# double >> appends rather than overwriting
echo "sinan" >> newfile.txt
```

### stdin(Standard IN)
By default, program receives its stdin from keyboard but you can change that.

Every command-line process in Linux operates with at least two fundamental data streams: standard input (stdin) and standard output (stdout). A program reads data from stdin and writes its results to stdout. 

```bash
# take peanuts.txt as input rather than keyboard.
cat < peanuts.txt
```

### stderr
It's default output stream to send error messages. Different from stdout. By default it send messages to terminal.

### Understanding File Descriptors
To manage I/O streams like stdin,stdout and stderr, the system uses file descriptors.

A file descriptor is a non-negative number that the kernel uses to identify an open file or stream. The default file descriptors are:
- 0: stdin
- 1: stdout
- 2: stderr

### Redirecting stderr to a File
```bash
# 2> -> error file descriptors
ls /fake/dict 2> peanuts.txt
```

### Combining stdout and stderr
```bash
ls /fake/dic /etc/passwd > peanuts.txt 2>&1
```
let's break this down:
- "> peanuts.txt" redirects stdout to the peanuts.txt
- "2>&1" redirects stderr to the same location that stdout currently pointing to. Order is important.

Modern and shorter way
```bash
ls /fake/dic /etc/passwd &> peanuts.txt
```

### Discarding Error Messages
```bash
# /dev/null discards any data writton to it
ls /fake/dic 2> /dev/null
```

### Pipe and tee
The pipe operator(|) takes the stdout of the command of its left 
and uses it as stdin for the command of its right.
```bash
ls -la /etc | less
```

### Splitting Output with Tee Command
See output on your screen and save it to a file
```bash
ls | tee peanuts.txt
```

### Combining Pipe and Tee
A common pattern is to pipe to tee in the middle of a 
longer command.chain. This allows you to save an intermediate result while continung to process the data.
```bash
# saves it to txt also passes it along.
ls -la /etc | tee etc_listing.txt | grep "conf"
```

### env (Environment)
These variables contain useful data about your session and configurations.
```bash
# $<variable_name>
echo $HOME
```
```bash
# Look at all variables in your env
env
```

### PATH Variable
```bash
echo $PATH
```
This command returns colon seperated list of directories. When you type a commands, your system searches through these directories to find corresponding executable file.

### Setting an Enviroment Variable for current session
```bash
export TEST=test
```
this variable will be available as long as the terminal sessios remains open.

### Making the Environment Variable Persistent
You need add it in .bashrc file.
- nano ~/.bashrc
- Add line to the end of the file: export TEST=test

### cut
```bash
# 5th char from each line
cut -c 5 sample.txt
# cutting by field (default TAB)
cut -f 2 sample.txt
# custom delimiters
cut -f 1 -d ";" sample.txt
```

### paste
merges lines together.
```bash
# default delimiter is TAB
paste -s sample2.txt
paste -d ' ' -s sample.txt
```

### head and tail
by default first/last 10 lines
"-n 15" -> first/last 15 lines

### Real-Time File Monitoring with tail -f
As new data appended it prints to the screen.
```bash
tail -f /var/log/syslog
```

### expand and unexpand
expand -> converts tabs into spaces
unexpand -> converts spaces back into tabs. 
unexpand in default only converts leading spaces of each line.
"-a" converts all 8 spaces into tab.

### join and split
join -> merges line from two files based on common field.
split -> breaks a large file into smaller ones. 
```
file1.txt
1 John
2 Jane
3 Mary

file2.txt
1 Doe
2 Doe
3 Sue
```
```bash
join file1.txt file2.txt
# 1 John Doe
# 2 Jane Doe
```
You specify different join fields.
```bash
join -1 2 -2 1 file1.txt file2.txt
```

By defaults, split commdand split file into new files once 1000 line limit is reached.
You can change this behavior with (-l or -b) flags.

### sort
```bash
# sort lines
sort file1.txt
# reverse sort
sort -r file1.txt
# sort by numerical value
sort -n file1.txt
```

### tr (Translate)
```bash
# lower case to upper case
echo "hello world" | tr a-z A-Z
# deleting characters
echo "My address is 2343" | tr -d '0-9'
# squeezing repeated chars
echo "Hello.  world, how are. you" | tr -s ' '
```

### uniq 
Caution: Only adjacent lines. So first sort the file.
```bash
# remove repeating adjacent lines
uniq reading.txt
# count the occurences of each line
uniq -c reading.txt
# display only the lines that are not repeated
uniq -u reading.txt
# disply only the repeating lines
uniq -d reading.txt
```

### wc and nl
```bash
# 1. Nr of lines 2. Nr of words 3. Nr of bytes
# you can get specific one with -l, -w, -c
wc /etc/passwd
```
nl -> add number of lines of the text

### grep 
searches for a pattern within. a file.
```bash
grep fox sample.txt
```

### Advanced Pattern Matching with grep -e
```bash
# good for searching patterns with "-"
grep -e "-v" file.txt
```

### Useful Grep Flags
- "-i" -> Case-insensitive search
- "-c" -> count matching lines
- "-o" -> show only the match
- "-f" -> patterns from a file

You can also use regex.