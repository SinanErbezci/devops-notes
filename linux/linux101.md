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