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


### Regex
"^" -> matches beginning of a line
"$" -> matches end of a line
"." -> match single char
"[]" -> char sets
"[^]" -> except those chars
"[a-c]" -> char ranges

### Vim
#### Searching and Navigation
/searched-word -> first occurence after cursor point
?searched-word -> same but backwards search
n -> jump to next match
h -> left or arrow keys
j -> right
k -> up
l -> down

#### Vim Inserting and Appending Text
There are two modes:normal for executing commands and insert mode for typing.

To go back normal mode use "Esc" key.

"i" -> insert current position
"a" -> append text after cursor
"I" -> at the beginning of the line
"A" -> at the end of line
"o" -> add new line below
"O" -> add new line above

#### Vim Operators and Motions
operator + motion.

dw -> d is operator action (delete) and w is movement (word).

You can also count. 2dw -> delete two words

x -> Delete char 
dw -> delete cursor to the beginning of next word
d$ -> cursor to the end of line
dd -> entire current line

cw – Changes the text from the cursor to the end of the word.
c$ – Changes text from the cursor to the end of the line.
cc – Changes the entire current line.

yw – Yanks (copies) a word.
yy – Yanks the entire current line.
p – Puts (pastes) the yanked text after the cursor or on the line below.
P – Puts the text before the cursor or on the line above.

r{char} – Replaces the single character under the cursor with the specified character.
R – Enters Replace mode, allowing you to overwrite text continuously until you press Esc.
J – Joins the current line with the next one.
. – Repeats the last change you made, a very powerful and efficient command.

:w -> saves the current stat
:q -> quit only if you saved
:q! -> quit and discard any changes
:wq -> save and quit
:u -> undo last action,

## User Management
Every user on a Linux system is assigned a personal home directory generally located at **/home/username**. User specific and configs are stored there.

The system identifies users with user id(UID) and groups id (GID).

The root user has unlimited power, capable of accessing any file and managing any process.

Authorized users can execute commands with root privileges using **sudo** (superuser do).

### root
**su** (subsitute user) command open new shell session for the linux root user. Also you can switch to any user with this command.

Actions performed in a root shell are not logged under your personal user account, making it difficult to audit system changes.

Who can access sudo privilege? **/etc/sudoers/** This file lists users and groups who grantted access.

### /etc/passwd
The mapping between username and UIDs is stored in **/etc/passwd/**.

#### Dissecting the /etc/passwd Fields
```
root:x:0:0:root:/root:/bin/bash
```
let's break down:
- Username: The login name of the user(root)
- Password: A placeholer of users encrypted password.
x -> encrypted password | * -> locked and cannot login | blank -> no passwprd
- User ID(UID): num id (root always 1)
- Group Id: primary group
- GECOS Field: Comment field.
- Home directory: user directory
- Default shell: executed upon login

### /etc/shadow
Stores sensitive user authentication info. Needs superuser privilege

User passwords and password aging policy.
```
root:MyEPTEa$6Nonsense:15000:0:99999:7:::
```
Lets break it down:
- Username: login name
- encrypted password: hashed user password. ! or * -> locked
- Date of last password change: The number of days since January 1, 1970
- Min password age: min days must pass before user can change their password again.
- Max password age: max days the password is valid.
- Password warning period
- Password inactivity period: 
- Account expiration date
- reserved field

### /etc/group
List of all user groups.
```
root:*:0:pete
```
- Group name
- Group password: legacy feature
- Group ID
- List of users

## File Permissions
**drwxr-xr-x**. 
Has 4 main parts. First char is file type. d -> dictionary, - -> file
d | rwx | r-x | r-x
r: read permisson
w: write permission
x: execute permission
-: no permission

First set -> User(owner)
Second set -> Group associated with the file
Third set -> all other users

### Modifying Permissons
#### Symbolic Mode
```bash
# adds executable permission to user
chmod u+x myfile
```
"+" -> add permission "-" -> remove permission

Also you can add multiple permission at once
```bash
chmod ug+w myfile
```
#### Numerical Mode
- 4 -> read(r)
- 2 -> write(w)
- 1 -> execute(x)

To set a permission set, you add numbers together.

4 + 2 + 1 = 7. So 7 gives all the permission
```bash
# user  rwx, group r-x, others r-x
chmod 755 myfile
```

## Ownership Permissions
```bash
# give ownership of the file to patty
sudo chown patty myfile
```
```bash
# change group ownership
sudo chgrp whales myfile
```
```bash
# both at the sametime
sudo chown patty:whales
```

### Umask
Every file that gets created comes with a default set of permissions. If you ever want to change that default set of permissions, you can do so with the umask command. 
```bash
# this takes away permissions
# user -> all access, group -> no write, others -> no execute
umask 021
```

### Setuid
Every file that gets created comes with a default set of permissions. If you ever want to change that default set of permissions, you can do so with the umask command.

-rwsr-xr-x

s -> suid. when a file has this permission set, it allows the users who launched the program to get the file owner's permission as well as execution permission

#### Modifying SUID
```bash
sudo chmod u+s myfile
sudo chmod 4755 myfile
```

### Setgid
samething but with group. Run as if it were a member of that group.
```bash
sudo chmod g+s myfile
sudo chmod 2555 myfile
```

### Process Permissions
There are three UIDs associated with every process.

When you launch a process, it runs with the same permissions as the user or group that ran it. This is known as an **effective user ID**. This UID is used to grant access rights to a process. So, naturally, if Bob ran the touch command, the process would run as him, and any files he created would be under his ownership.

There is another UID, called the **real user ID**. This is the ID of the user that launched the process. These are used to track down who the user who launched the process is.

One last UID is the **saved user ID**. This allows a process to switch between the effective UID and real UID, and vice versa

### The Sticky Bit
The sticky bit is a permission setting that can be applied to a directory. When a directory has the sticky bit set, files within that directory can only be deleted or renamed by the file's owner, the directory's owner, or the root user. This is particularly useful for shared directories where multiple users need to create and manage their own files without interfering with others.
```bash
# drwxrwxrwt 
chmod +t my_shared_dir
chmod 1755 my_shared_dir
```


## Processes
Each process is assigned a unique number called the process ID (PID). PIDs are typically assigned sequentially as new processes are created.
```bash
ps
```
```
$ ps
PID        TTY     STAT   TIME          CMD
41230    pts/4    Ss        00:00:00     bash
51224    pts/4    R+        00:00:00     ps
```
- PID: Process ID
- TTY: Controlling terminal for the process
- STAT: Current status of the process
- TIME: Total CPU time process has used
- CMD: the command that started the process

#### Other options
```bash
ps aux
```
a -> displayy all process for all users
u -> detailed, user-oriented format
x -> Includes proccess not attached to any terminal.
```bash
# System V style
ps -ef
```

#### Real Time monitoring with top
real time 
```bash
top
```

### Controlling Terminal
TTY refers to the terminal that provides the standard input and output for a process.

There are two main types of terminals you will encounter: terminal devices and pseudo-terminal devices.

A true terminal device is a native console that allows you to type commands and see output directly. You can experience this by switching to a virtual console. On many systems, you can press Ctrl-Alt-F1 to access TTY1. To return to your graphical session, you can typically use Ctrl-Alt-F7.

A pseudo-terminal (PTS), on the other hand, is what you most commonly use. When you open a terminal application within your graphical desktop environment, you are using a PTS. These emulate a terminal within a window.

Most processes are bound to a controlling terminal. This means the process's lifecycle is tied to the terminal session that started it.

Some processes, known as daemons, are designed to run in the background and manage system services. These processes often start when the system boots and stop only when it shuts down. To prevent them from being accidentally terminated, daemons are not attached to a controlling terminal. (you will see a question mark (?) in the TTY column. )

* look for more details

### kill (terminate)
```bash
# kill <pid>
kill 12345
```
#### Forcing Termination with SIGKILL
```bash
# Forcefull termination. Without giving it a chance of clean up.
kill -9 12345
```
#### Understanding Other Common Signals
- SIGHUP:  (signal 1) traditionally sent to a process when its controlling terminal is closed. It can be used to tell daemon processes to reload their configuration files.
- SIGINT: (signal 2) Sent when you enter Ctrl+C.
- SIGSTOP: (signal 19) Pauses process without terminating.
```bash
#  checks if a process with the specified PID exists
kill -0 12345
```

### niceness
The niceness of a process is represented by a number ranging from -20 (highest priority) to 19 (lowest priority).

A high niceness value (e.g., 19) means the process is very "nice" and has a low priority, yielding CPU time to others.
A low or negative niceness value (e.g., -20) means the process is not "nice" and demands more CPU time, giving it a higher priority.clear
```bash
# look at ni column
top
```
```bash
nice -n 5 apt update
# change niceness already running process
renice 10 -p 12345
```

### Process States
R -> Running or Runnable.
S -> Interruptiple Sleep. Process is waiting for an event to complete.
D -> Uninterruptiple Sleep. Cannot be interrupted by a signal.
Z -> Zombie. It is waiting for its parent process to read its exit status
T -> Stopped. Suspended by a signal. Can be continued with SIGCONT.

### /proc filesystem
In linux everything is treated as a file. This concept extends to running processes, whose information is dynamically stored in a special virtual filesystem known as /proc.

The /proc filesystem is not a real filesystem on your hard drive; it's created in memory by the kernel. It provides a window into the kernel's internal data structures and the state of the system.

### Job Control
You can manage multiple background processes with a single terminal.

"&" -> this immediately returns shell prompt while first command continues to run.
```bash
sleep 1000 &
sleep 1001 &
sleep 1002 &
```

```bash
# list all background jobs
jobs
```

Also during the program is running you can type **Control + Z** then use the **bg** command to send that suspended job to background. 

Also you can move it to foreground by **fg %(job_id)**.

### tar and gzip
tar -> archiving, gzip -> compression
```bash
gzip myfile
gunzip myfile.gz
# c-> new acrhive, v->verbose, f-> next argument name of the tar
tar cvf myarchive.tar file1 file2 file3
# compressed tar 
tar cvzf 
# extract compressed tar
tar xzvf myarchive.tar.gz
```

## Devices
In Linux, every device connected to your system, from hard drives to keyboards, is represented by a special file.

These files, known as device files or device nodes, provide a way for software to interact with the hardware drivers. The central location for these files is the /dev directory.

### /dev directory
It contains special files that represent devices.
```bash
# list devices
ls /dev
```
/dev/null -> special device that ignores all inputs

### Device Types
```bash
ls -l /dev
# Major device number -> driver responsible for the device
# minor device number -> instance of the device
```
First char in the permission string indicates file type.
- c -> char. Transfer data one char at a time. Many OS functions.
- b -> block. transfer data in blocks. Hard drives, ssds
- p -> pipe. fifo. inter-process com.
- s -> socket. more versatile.

### Device Names
Linux controls storage devices through SCSI(Small Computer System Interface).

That's why storage device name starts with **sd**.

/dev/sda3 -> sd: mass storage device, a:first device, 3:partition

PseudoDevices -> not real physical devices but system functions.

/dev/random: stream of random numbers
/dev/null: discards all input and no output
/dev/zero: discards all input output NULL bytes.

### sysfs
It is a virtual filesystem, mounted at /sys. Exports info about kernel objects, hardware devices and drivers.

Represent the current state of the sys system.

### /sys Directory
Gives info about:
- manufacturer and model,
- where the device plugged in,
- current state, position in the device hieararchy.

### sysfs vs /dev
/dev -> device nodes which are special files that allow programs to access the devices
/sys -> view info and manage the devices. Underlying model of the device.

### udev
The udev system dynamically creates and removes devices. No need manually add and remove devices.

###  lsusb, lspci, lsscsi
lsusb -> listing usb devices
lspci -> pci devices
lsscsi -> scsi and sata (storage)

### dd
Reads for file or datastream, writes to output file and datastream.

```bash
# if:input file, of:output file, bs:block size
dd if=/home/pete/backup.img of=/dev/sdb bs=1024
```

## The file systems
### The Main Directories
- /bin -> essential commandline programs(ls, cp etc.)
- /sbin -> essential system binaries.
- /etc -> core system config directory. no exec only config for system and apps
- /lib -> essential shared library files.
- /boot -> files required for system boot
- /home -> personal directory for each user
- /root -> home directory for root user
- /opt -> optional or third part application software packages.
- /usr -> user-installed software and packages.
- /var -> variable and stores files that are expected to change in size. (system logs, caches etc)
- /tmp -> files in this deleted upon system reboot
- /run -> Running system info (pids, runtime data etc)
- /dev -> device files
- /media -> removable media like usb, sd cards, cd-roms
- /mnt -> generic mount point for temporarily mounting filesystems
- /proc -> virtual filesystem realtime info about proccess and kernel paramaters
- /srv -> site-specific data such as files for a web server
### Filesystem Types
linux supports wide range of filesystems. To work seamlessly with different filesystem, linux uses Virtual file system(VFS).

common file system types:
- ex4: Linux extended filesystem.
- btrfs: B-tree FS. with advanced features
- XFS: large files and parallel I/O.
- NTFS and FAT: standard windows filesystem.
- HFS+: macOS
```bash
# list your filesystem
df
```

### Disk Partitioning
- fdisk: basic command line partitioning tool. not support GPT
- parted: support both MBR and GPT
- gparted: graphical version of parted.
- gdisk: only support GPT
```bash
# listing existing partitions
sudo parted -l
```
```bash
# launching interactive mode
sudo parted
```
```bash
#select the disk you want to modify
select /dev/sdb
# viewing the partition table
print
# creating a partition
mkpart primary ext4 1MB 5000MB
# resizing a partition
resizepart 1 8000MB
```
### Creating Filesystem(Formatting)
```bash
mkfs -t ext4 /dev/sdb2
```

### Mounting and Unmounting
```bash
# First create a mount point
mkdir /mydrive
# Attach device
sudo mount -t ext4 /dev/sdb2 /mydrive
```
```bash
umount /mydrive
```

Kernel names of the device can change with reboots. To avoid issues, use UUID.
```bash
# view block device UUIDs
blkid
# mount with UUID
mount UUID=<...> /mydrive
```

### Mounts filesystem at startup
You configure them in a special configuration file at **/etc/fstab**.

This file contains a permanent list of filesystems that the system should mount during the boot process.

#### /etc/fstab
```plaintext
pete@icebox:~$ cat /etc/fstab
UUID=130b882f-7d79-436d-a096-1e594c92bb76 /               ext4    relatime,errors=remount-ro 0       1
UUID=78d203a0-7c18-49bd-9e07-54f44cdb5726 /home           xfs     relatime        0       2
UUID=22c3d34b-467e-467c-b44d-f03803c2c526 none            swap    sw              0       0
```
let's break down:
- Device Identifier: UUID
- Mount point: / or /home
- Filesystem Type: ex4, xfs etc.
- Options: how the filesystem is mounted. Different options.
- Dump: if a file system needs to backed up.
- Pass: order for checking filesystems at boot time. 0 -> no checkhing

### swap
allocate virtual memory on disk.

### Disk Usage
```bash
# Checking Filesystem space with df
df -h
# Disk usade for each subdirectory in your current location
du -h
```

### Filesystem Repair
**fsck** -> check consistency of a filesystem

### Inodes
Every file and directory has its own inode. It's metadate that describes:
- file type
- owner, group
- permissions etc.

If you run out of inode space, you cannot create new files. check it with **df -i**.

check inode number with **ls -li**.

### File Links
There are two type of links: symlink, hard links.

symlink -> it's the same with shortcuts in windonws.
hardlink -> creates another file entry that points directly to the same inode as the original file.
```bash
# symlink
ln -s /path/to/original /path/to/link
# hardlink
ln /path/to/original /path/to/link
```

## Boot Process Overview
BIOS -> Bootloader -> Kernel -> Init
Bootloader -> load kernel into memory. Configure kernel parameters
Kernel -> loading drivers, locating boot and starting init
init -> Parent of all other processes. 3 different ways (System V, Upstart, systemd)

## Tracking Procceses: top
top -> tracking processes in real time
lsof -> list of all open files and proccesses using them
```bash
# processes are using the current directory.
lsof .
```
fuser -> which processes using specific files, sockets or filesystems.
```bash
# kill all processes  using a mount point
fuser -k /mnt/usb
```

### uptime
uptime -> load average: 0.00. 0.02, 0.05 -> 1, 5, 15 min interval

### Other Montioring Tools
I/O Monitoring -> iostat
Memory Moninotring -> vmstat
Continous Monitoring -> sar

### Cron Jobs
```plaintext
Cron Job Syntax
30 08 * * * /home/pete/scripts/change_wallpaper
```
First 5 are time and date fields. "*" meaning every.
So this means this command runs at 8:30 Am, every day of the month, every month, everyday of the week.

```bash
# edit your cron jobs
crontab -e
```

## Logging
syslog -> core service responsible for gathering info
rsyslogd -> daemon, waiting for event messagaes.
dmesg -> kernel logging. For hardware issues
auth.log -> authentication logging
logrotate -> log rotation.