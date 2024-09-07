# Linux I/O redirection and piping.

1. Basic Concepts
2. Input Redirection
3. Output Redirection
4. Error Redirection
5. Piping
6. Advanced Techniques

## 1. Basic Concepts:

In Unix/Linux, there are three standard streams:
- Standard Input (stdin): 0
- Standard Output (stdout): 1
- Standard Error (stderr): 2

By default, stdin is the keyboard, while stdout and stderr are both the terminal.

## 2. Input Redirection:

The < symbol is used for input redirection.

Example:
- `sort < file.txt` # This command sorts the contents of file.txt.

## 3. Output Redirection:

The > symbol is used for output redirection. It creates a new file or overwrites an existing one.
The >> symbol appends to an existing file or creates a new one if it doesn't exist.

Examples:
- `echo "Hello, World!" > greeting.txt` # Create or overwrite file called "greeting.txt" with "Hello World!"
- `echo "How are you?" >> greeting.txt` # Append or addon to the end of "greeting.txt" with "How are you?"

## 4. Error Redirection:

You can redirect stderr using 2> or 2>>.

Example:
- `ls /nonexistent 2> error.log` # pipe the error log from the `ls` command into "./error.log"

To redirect both stdout and stderr to the same file:
- `command > output.log 2>&1`

## 5. Piping:

The | symbol is used for piping. It sends the output of one command as input to another.

Example:
- `ls -l | grep "\.txt"` # This lists all files and then filters for those ending in .txt.

## 6. Advanced Techniques:

### a) Here Documents:
```
cat << EOF > file.txt
Line 1
Line 2
EOF
``` 
#This will write "Line 1 Line2" into "file.txt" and only stop writing new data when it reaches the line "EOF" (End Of File)

- b) Process Substitution:
- `diff <(ls dir1) <(ls dir2)`

- c) Redirecting stdout and stderr to different files:
- `command 1> output.log 2> error.log`

- d) Discarding output:
- `command > /dev/null 2>&1`

- e) tee command (writing to both file and stdout):
- `echo "Hello" | tee file.txt` # This command will wrte "Hello" to stdout (screen) and to the file "file.txt" simultaneously

- f) Named Pipes (FIFOs):
- `mkfifo mypipe`
- `command1 > mypipe & command2 < mypipe`