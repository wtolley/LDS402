# Basic Commands and Directory Hierarchy

- **Focus**: Introduces essential Unix commands, directory structures, and the foundational building blocks of interacting with a Linux system.
- **Why Unix Commands?**
  - Linux is a Unix-based system; understanding core Unix commands gives you transferrable skills for other Unix-flavored systems (e.g., BSD).
  - Mastering core Unix commands will enable you to better understand the inner workings of Linux.

---

# The Bourne Shell: /bin/sh
- **Shell**: Command interpreter and programming environment for running commands and automating tasks.
  - **Shell Commands**: A command typed into the terminal, like `echo`, executes programs.
  - **Shell Scripts**: A series of shell commands stored in a file (text file with executable commands).
  - **Common Shells**: Bourne Shell (`sh`), Bourne-Again Shell (`bash`), Z shell (`zsh`).
  - **Bash** is an enhanced version of the Bourne shell, commonly the default shell on Linux systems.

---

# Using the Shell
- **Opening a Shell**: Terminal emulators such as GNOME Terminal or KDE Konsole open a shell window.
- **Shell Prompt**: Indicates readiness for user commands.
  - Example: `name@host:path$`, where:
    - **name**: your username,
    - **host**: machine name,
    - **path**: current directory.
- **Basic Commands**:
  - `$ echo Hello there.`: Outputs `Hello there.` to the terminal.
  - `$ cat /etc/passwd`: Displays contents of the `/etc/passwd` file.
  
---

# File and Directory Operations
- **ls**: List directory contents.
  - `ls`: Basic listing of current directory.
  - `ls -l`: Long listing with detailed file information (permissions, owner, size).
  - `ls -F`: Shows file type (e.g., `/` for directories, `*` for executables).
  - Example: `$ ls -l /home/user/` lists all files in the `/home/user/` directory in a detailed view.

---

# File Manipulation Commands
- **cp**: Copy files or directories.
  - Usage: `cp file1 file2` (copies `file1` to `file2`).
  - Example: `$ cp /home/user/file.txt /backup/` (copies file.txt to `/backup/` directory).
- **mv**: Move or rename files.
  - Example: `$ mv file1.txt file2.txt` (renames `file1.txt` to `file2.txt`).
  - Example: `$ mv file1.txt /newdirectory/` (moves `file1.txt` to `/newdirectory/`).
- **rm**: Remove files or directories.
  - Example: `$ rm file.txt` (deletes the `file.txt`).
  - Use `rm -r` to recursively delete a directory and its contents.
  - Caution: This is a permanent deletion with no undo.
  
---

# Creating and Modifying Files
- **touch**: Create an empty file or update the modification time of an existing file.
  - Example: `$ touch newfile.txt`.
- **echo**: Print text to the terminal or append it to files.
  - Example: `$ echo "Hello" > file.txt` (creates or overwrites `file.txt` with "Hello").
  - Example: `$ echo "Hello" >> file.txt` (appends "Hello" to the end of `file.txt`).

---

# Streams and Redirection
- **Input/Output (I/O) Streams**:
  - **stdin**: Standard input (usually from the keyboard).
  - **stdout**: Standard output (usually the terminal).
  - **stderr**: Standard error output (for error messages).
  
- **Redirection**:
  - **Output Redirection**: `$ command > file` redirects stdout to a file.
    - Example: `$ ls > list.txt` saves the directory listing in `list.txt`.
  - **Append Output**: `$ command >> file` appends output to a file.
    - Example: `$ echo "New entry" >> logfile.txt`.
  - **Pipe**: `$ command1 | command2` sends the output of `command1` to `command2`.
    - Example: `$ cat file.txt | grep "word"` (searches for "word" in `file.txt`).

---

# Navigating the Filesystem
- **cd**: Change directory.
  - `$ cd /path/to/directory` moves to the specified directory.
  - `$ cd ..` moves up one level in the directory hierarchy.
  - `$ cd` (with no argument) returns to the home directory.
- **pwd**: Print working directory.
  - Displays the full path of the current directory.
  - Example: `$ pwd` might return `/home/user/`.

---

# Directory Operations
- **mkdir**: Create new directories.
  - Usage: `$ mkdir newdir`.
  - Example: `$ mkdir /home/user/newdir` (creates `newdir` inside `/home/user/`).
- **rmdir**: Remove empty directories.
  - Usage: `$ rmdir dir` (only works if the directory is empty).
  - **rm -r dir**: Recursively delete directories and their contents.
  - **Caution**: Be very careful using `rm -r`, especially as root.

---

# File Permissions and Ownership
- **Understanding File Permissions**:
  - **File Modes**: `r` = read, `w` = write, `x` = execute.
  - Permissions are shown with `ls -l`, e.g., `-rwxr-xr--`.
    - First part: type (`-` = file, `d` = directory, `l` = symbolic link).
    - Next three parts: permissions for user, group, others.
- **chmod**: Change file permissions.
  - Example: `$ chmod 755 file` (user can read, write, execute; group/others can read, execute).
  - Usage: `chmod [permissions] [file]`.
- **chown**: Change file ownership.
  - Example: `$ chown user:group file`.
  
---

# Symbolic Links
- **ln -s**: Create a symbolic (soft) link to a file or directory.
  - Example: `$ ln -s /usr/local/bin/script.sh ~/bin/myscript` creates a link to `script.sh`.
  - Symbolic links are shortcuts pointing to files/directories, useful for organizing and accessing files from different locations.

---

# Intermediate Commands
- **grep**: Search for a pattern in files.
  - Usage: `grep [pattern] [file]`.
  - Example: `$ grep root /etc/passwd` (searches for lines containing "root").
  - Options: `-i` (case-insensitive), `-v` (invert match).
- **find**: Search for files within a directory hierarchy.
  - Example: `$ find /home -name "*.txt"` (finds all `.txt` files in `/home`).
- **head/tail**: View the first or last lines of a file.
  - Example: `$ head -n 10 file.txt` (shows first 10 lines).
  - Example: `$ tail -n 10 file.txt` (shows last 10 lines).

---

# Shell Globbing (Wildcards)
- **Wildcards for Pattern Matching**:
  - `*` matches any string of characters.
  - `?` matches exactly one character.
- **Examples**:
  - `$ echo *.txt` (lists all `.txt` files in the current directory).
  - `$ ls at*` (lists all files starting with "at").
  - `$ ls *.c` (lists all `.c` files).

---

# Process Management
- **ps**: Display running processes.
  - Example: `$ ps aux` (lists all processes running on the system).
  - Shows process ID (PID), user, CPU/memory usage, command.
- **kill**: Send a signal to terminate a process.
  - Example: `$ kill PID` (sends TERM signal to terminate a process).
  - Example: `$ kill -9 PID` (forcefully terminates a process with KILL signal).
- **Job Control**:
  - Use `&` to run a command in the background, e.g., `$ command &`.
  - Use `fg` to bring background processes to the foreground.
  
---

# Archiving and Compression
- **tar**: Archive files into a single file.
  - Example: `$ tar cvf archive.tar file1 file2` (creates `archive.tar` from `file1` and `file2`).
  - **Extract**: `$ tar xvf archive.tar` (extracts the files from the archive).
- **gzip**: Compress files.
  - Example: `$ gzip file` (compresses `file` into `file.gz`).
  - **gunzip**: Decompress `.gz` files.

---

# Linux Directory Hierarchy Essentials
- **Filesystem Hierarchy Standard (FHS)**:
  - `/`: Root directory containing all other directories.
  - `/bin`: Essential binaries for all users.
  - `/usr`: User programs and applications.
  - `/var`: Variable files such as logs, temporary files.
  - **Explore the system**: Start with `ls /` to examine the directory structure.
``
