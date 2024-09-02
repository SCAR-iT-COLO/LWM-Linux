# Basic Shell (Bash)

### 1. Introduction to Bash and the command line

Bash (Bourne Again SHell) is a command-line interface and scripting language used in Unix-like operating systems, including Linux. It's an improved version of the original Bourne Shell (sh).

Key points about Bash:
- It's the default shell in most Linux distributions.
- It allows users to interact with the operating system through text commands.
- It's both an interactive shell and a scripting language.

To start using Bash:
1. Open a terminal window in your Linux distribution.
2. You'll see a prompt, typically ending with a $ symbol for regular users or # for root users.

Basic syntax:
```
command [options] [arguments]
```

For example:
```bash
ls -l /home/user
```
Here, 'ls' is the command, '-l' is an option, and '/home/user' is an argument.

Some essential commands to get started:
- `echo`: Prints text to the screen
  Example: `echo "Hello, World!"`

- `date`: Displays the current date and time
  Example: `date`

- `cal`: Shows a calendar
  Example: `cal` or `cal 2024` for a specific year

- `man`: Displays the manual page for a command
  Example: `man ls` (Use 'q' to exit)

### 2. Basic navigation and file management

Linux file system hierarchy:
The file system in Linux is organized in a tree-like structure, starting from the root directory (/).

Key directories:
- /: Root directory
- /home: User home directories
- /etc: System configuration files
- /var: Variable data (logs, temporary files)
- /bin: Essential command binaries
- /usr: User programs and data

Navigation commands:
- `pwd`: Print Working Directory
  Example: ```bash
  pwd
  ```

- `cd`: Change Directory
  Examples:
  ```bash
  cd /home/user
  ```
  cd ..  # Move up one directory
  cd ~   # Move to home directory
  cd -   # Move to previous directory
  ```

- `ls`: List directory contents
  Examples:
  ```bash
  ls
  ls -l  # Long format
  ls -a  # Show hidden files
  ls -lh # Human-readable file sizes
  ```

File and directory management:
- `mkdir`: Create a new directory
  Example: `mkdir new_folder`

- `touch`: Create an empty file or update timestamp
  Example: `touch newfile.txt`

- `cp`: Copy files or directories
  Examples:
  ```bash
  cp file.txt /path/to/destination/
  cp -r folder/ /path/to/destination/  # Recursive copy for directories
  ```

- `mv`: Move or rename files/directories
  Examples:
  ```bash
  mv file.txt newname.txt  # Rename
  mv file.txt /new/location/  # Move
  ```

- `rm`: Remove files or directories
  Examples:
  ```bash
  rm file.txt
  rm -r folder/  # Remove directory and contents
  rm -i file.txt # Interactive mode (asks before deleting)
  ```

- `cat`: Concatenate and display file contents
  Example: `cat file.txt`

- `less`: View file contents page by page
  Example: `less longfile.txt` (Use 'q' to exit)

- `head` and `tail`: View the beginning or end of a file
  Examples:
  ```bash
  head -n 5 file.txt  # First 5 lines
  tail -n 10 file.txt # Last 10 lines
  ```

File permissions:
Linux uses a permission system for files and directories. You can view permissions with `ls -l`:
```
-rw-r--r-- 1 user group 1234 Jan 1 12:00 file.txt
```

The first 10 characters represent:
- File type (- for regular file, d for directory)
- Read (r), Write (w), and Execute (x) permissions for Owner, Group, and Others

To change permissions, use the `chmod` command:
```bash
chmod u+x script.sh  # Add execute permission for the owner
chmod 644 file.txt   # Set specific permissions (rw-r--r--)
```
