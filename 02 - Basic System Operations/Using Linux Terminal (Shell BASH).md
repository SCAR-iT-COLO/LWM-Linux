# Using the Linux Terminal (BASH Shell)

## 1. **Opening the Terminal**:
   - You can open the terminal in various ways:
     - **Shortcut**: Press `Ctrl + Alt + T`.
     - **Application Menu**: Search for "Terminal" in your applications.
     - **Command**: Use the `gnome-terminal` command.
     
## 2. Basic Navigation:
   - pwd: Print working directory
   - ls: List files and directories
   - cd: Change directory
   - mkdir: Create a new directory
   - rmdir: Remove an empty directory
   - touch: Create an empty file

## 3. File Operations:
   - cp: Copy files or directories
   - mv: Move or rename files/directories
   - rm: Remove files or directories
   - cat: Display file contents
   - less: View file contents page by page
   - head/tail: View beginning/end of a file

## 4. Text Editing:
   - nano: Simple text editor
   - vim: Advanced text editor
   - emacs: Another advanced text editor

## 5. File Permissions:
   - chmod: Change file permissions
   - chown: Change file owner
   - chgrp: Change group ownership

## 6. Process Management:
   - ps: List running processes
   - top: Dynamic view of system processes
   - kill: Terminate a process
   - fg/bg: Bring process to foreground/background

## 7. System Information:
   - uname: Display system information
   - df: Show disk usage
   - du: Display directory space usage
   - free: Show memory usage

## 8. Network Commands:
   - ifconfig: Configure network interfaces
   - ping: Test network connectivity
   - ssh: Secure shell for remote access
   - scp: Securely copy files between hosts

## 9. Package Management:
   - apt-get (Debian/Ubuntu): Install, update, remove packages
   - yum (CentOS/Fedora): Similar to apt-get
   - dnf (Fedora): Next-generation package manager

## 10. File Compression:
   - tar: Archive files
   - gzip/gunzip: Compress/decompress files
   - zip/unzip: Create/extract zip archives

## 11. Text Processing:
    - grep: Search for patterns in files
    - sed: Stream editor for text manipulation
    - awk: Pattern scanning and text processing

## 12. Redirection and Pipes:
    - >: Redirect output to a file OVERWRITING original file if it exists
    - >>: Append output to a file or create a new file.
    - <: Read input from a file
    - |: Pipe output of one command to another "command chaining"

## 13. User Management:
    - useradd: Add a new user
    - userdel: Delete a user
    - passwd: Change user password

## 14. Advanced Commands:
    - find: Search for files in a directory hierarchy
    - xargs: Build and execute command lines from standard input
    - sort: Sort lines of text
    - uniq: Report or omit repeated lines

## 15. Shell Scripting:
    - Variables: var_name=value
    - Conditionals: if, elif, else
    - Loops: for, while
    - Functions: function_name() { commands; }

## 16. Job Control:
    - jobs: List active jobs
    - &: Run a command in the background
    - Ctrl+Z: Suspend a running process
    - Ctrl+C: Terminate a running process
