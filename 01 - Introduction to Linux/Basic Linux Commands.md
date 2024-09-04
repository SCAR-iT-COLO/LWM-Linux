
# Basic Linux Commands

## 1. Navigation and File Management:

### a) pwd (Print Working Directory)
   - Shows the current directory path
   - Usage: `pwd`

### b) ls (List)
   - Lists files and directories in the current directory
   - Usage: `ls` [options] [directory]
#### Common options:
   - l: Long format with details
   - a: Show hidden files
   - h: Human-readable file sizes

### c) cd (Change Directory)
   - Changes the current directory
   - Usage: 
   -  `cd [directory]`

### d) mkdir (Make Directory)
   - Creates a new directory
   - Usage: `mkdir [directory_name]`

### e) rmdir (Remove Directory)
   - Removes an empty directory
   - Usage: `rmdir [directory_name]`

### f) touch
   - Creates an empty file or updates timestamps
   - Usage: `touch [filename]`

### g) cp (Copy)
   - Copies files or directories
   - Usage: `cp [source] [destination]`
#### Common Options:
     -r: Recursive (for directories)

### h) mv (Move)
   - Moves or renames files and directories
   - Usage: `mv [source] [destination]`

### i) rm (Remove)
   - Deletes files or directories
   - Usage: `rm [options] [file/directory]`
#### Options:
     -r: Recursive (for directories)
     -f: Force deletion without prompting

## 2. File Viewing and Editing:

### a) cat (Concatenate)
   - Displays file contents
   - Usage: `cat [filename]`

### b) less
   - Views file contents page by page
   - Usage: `less [filename]`

### c) head
   - Displays the first few lines of a file
   - Usage: `head [options] [filename]`
#### Common Options:
     -n [number]: Specify number of lines

### d) tail
   - Displays the last few lines of a file
   - Usage: `tail [options] [filename]`
#### Common Options:
     -n [number]: Specify number of lines
     -f: Follow file updates in real-time

### e) nano
   - Simple text editor
   - Usage: `nano [filename]`

## 3. File Permissions and Ownership:

### a) chmod (Change Mode)
   - Modifies file permissions
   - Usage: `chmod [options] [mode] [file/directory]`
   
### b) chown (Change Owner)
   - Changes file ownership
   - Usage: `chown [user]:[group] [file/directory]`

## 4. System Information:

### a) uname
   - Displays system information
   - Usage: `uname [options]`
#### Common Options:
     -a: All information

### b) df (Disk Free)
   - Shows disk space usage
   - Usage: df [options]
#### Common Options:
     -h: Human-readable sizes

### c) du (Disk Usage)
   - Estimates file and directory space usage
   - Usage: `du [options] [directory]`
#### Common Options:
     -h: Human-readable sizes
     -s: Summary for directory

## 5. Process Management:

### a) ps (Process Status)
   - Lists running processes
   - Usage: `ps [options]`
#### Common options:
     -aux: Detailed information for all processes

### b) top
   - Displays real-time system process information
   - Usage: `top -u [user]`
#### Common Options:
     -u: active apps for specified user

### c) kill
   - Terminates processes
   - Usage: `kill [options] [PID]`
#### Common Options:
     -9: Force kill

## 6. Network Commands:

### a) ping
   - Tests network connectivity
   - Usage: `ping [options] [destination]`

### b) ifconfig
   - Displays network interface information
   - Usage: `ifconfig`

### c) ssh (Secure Shell)
   - Connects to remote systems securely
   - Usage: `ssh [user]@[host]`
#### Common Options:
     -p: Specify a port

## 7. Package Management (for Debian-based systems):

### a) apt-get update
   - Updates package lists
   - Usage: `sudo apt-get update`

### b) apt-get upgrade
   - Upgrades installed packages
   - Usage: `sudo apt-get upgrade`

### c) apt-get install
   - Installs new packages
   - Usage: `sudo apt-get install [package_name]`

## 8. File Compression:

### a) tar
   - Archives files
   - Usage: `tar [options] [archive_name] [files/directories]`
   - Usage: `tar -cvf archive.tar files/` "compress files from 'files' directory into archive.tar"
#### Common options:
     -c: Create archive
     -x: Extract archive
     -v: Verbose
     -f: Specify archive file
     -t: List the contents inside the tar file
     -z: Gzip the file after tar'ing it. "Double compressed"

### b) gzip
   - Compresses files
   - Usage: `gzip [filename]`

### c) gunzip
   - Decompresses gzip files
   - Usage: `gunzip [filename.gz]`
