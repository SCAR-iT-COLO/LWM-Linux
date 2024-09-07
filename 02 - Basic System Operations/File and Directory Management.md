# Linux File and Directory management

## 1. File System Hierarchy:
Linux follows a hierarchical file system structure, starting with the root directory (/). Key directories include:

- /home: User home directories
- /etc: System configuration files
- /var: Variable data (logs, temporary files)
- /usr: User binaries and program files
- /bin: Essential command binaries
- /sbin: System binaries
- /tmp: Temporary files

## 2. Basic Commands:

### - Listing files and directories:
`ls [options] [directory]`
Common options:
- -l: Long format
- -a: Show hidden files
- -h: Human-readable file sizes

### - Changing directories:
`cd [directory]`
- `cd ..`: Move up one directory
- `cd`: Go to home directory
- `cd /`: Go to root directory

### - Creating directories:
`mkdir [options] directory_name`
Common options:
- -p: Create parent directories if they don't exist

### - Removing directories:
`rmdir [options] directory_name`

### - Creating empty files:
`touch file_name`

### - Copying files and directories:
`cp [options] source destination`
Common options:
- -r: Copy directories recursively

### - Moving/renaming files and directories:
`mv source destination`

### - Removing files:
`rm [options] file_name`
Common options:
- -f: Force removal without prompting

## 3. File Permissions:

Linux uses a permission system with read (r), write (w), and execute (x) permissions for owner, group, and others.

### Viewing permissions:
`ls -l`

### Changing permissions:
`chmod [options] mode file`
Example: chmod 755 file_name "to make a file permissions RWX-Owner, RX-Group, RX-Others

### Changing ownership:
`chown [options] user:group file`

## 4. File Manipulation:

### Viewing file contents:
- `cat file_name` #Print entire file at once
- `less file_name` #View file in a pager format
- `more file_name` #View file in a pager format
- `head file_name` #View top 10 lines (default) of a file
- `tail file_name` #View last 10 lines (default) of a file


### Searching file contents:
`grep [options] pattern file`
Common options:
- -i: Insensitive Case Search
- -R: search recursively in parent Directory, as well as all child directories.
- -n: Return the line number in the file where the match occured

### Comparing files:
`diff file1 file2`

## 5. Advanced File Management:

### Finding files:
`find [path] [expression]`
Common Options:
- -iname: Insensitive case search
- -name: Case Sensitive search

Example: `find /home -name "*.txt"`

### Disk usage:
`du [options] [directory]`
Common options:
- -h: Print disk usage in human-readable format
- -s: Summarize disk usage information
- -S: Summarize disk usage by each sub-directory

### File compression and archiving:
`tar [options] files.tar files` #Create a tar archive called "files.tar" with everything in the "files" directory
`gzip -k file_name` #Create a gzipped archive while keeping the original file "-k"
`gunzip -k file_name.gz` #Extract a .gzip file while keeping "-k" the original archive.


### Symbolic links "Shortcuts":
`ln -s target_file link_name`

## 6. Text Editors:

- nano: Simple and user-friendly #Included with most distros by default
- vim: Advanced and powerful
- emacs: Extensible and feature-rich

## 7. File System Management:

### Mounting file systems:
`mount` [options] device directory

### Unmounting file systems:
`umount` [options] directory

### Checking disk space:
`df` [options]
Common Options:
- -h: Human-readable output

## 8. File System Maintenance:

### Checking and repairing file systems:
`fsck [options] device` #Not used with BTRFS filesystem

### Creating file systems:
`mkfs.[FSTYPE] [options] device` #Will erase device/disk if not entered correctly

## 9. Access Control Lists (ACLs):

### For more fine-grained permission control:
`getfacl file`
`setfacl -m u:user:rwx file`

## 10. Inode Information:

### View detailed file information:
`stat file_name`

## 11. External Sources:

- [(1) Linux File Management Series for Beginners - Linux Shell Tips.](https://www.ubuntumint.com/linux-file-management/.)
- [(2) Linux Commands Cheat Sheet {with Free Downloadable PDF} - phoenixNAP.](https://phoenixnap.com/kb/linux-commands-cheat-sheet.)
