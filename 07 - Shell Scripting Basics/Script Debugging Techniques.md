# Script Debugging Techniques

## 1. Enable debugging mode

The first step in debugging a bash script is to enable debugging mode. You can do this in two ways:

- Add the -x option when running the script:

```
bash -x your_script.sh
```

- Add the set -x command at the beginning of your script:

```
#!/bin/bash
set -x

# Rest of your script
```

The -x option enables trace debugging, which prints each command and its arguments as they are executed.

## 2. Use set options for additional debugging

Bash provides several set options that can help with debugging:

- `set -e`: Exit immediately if a command exits with a non-zero status.
- `set -u`: Treat unset variables as an error when substituting.
- `set -o` pipefail: The return value of a pipeline is the status of the last command to exit with a non-zero status.

You can combine these options:

```
#!/bin/bash
set -euo pipefail
set -x

# Rest of your script
```

## 3. Add echo statements

Insert echo statements throughout your script to print variable values or to indicate which part of the script is being executed:

```
echo "Debug: Variable value is $variable"
echo "Debug: Entering function foo"
```

## 4. Use bash's built-in debugging commands

Bash provides several built-in commands for debugging:

- `set -v`: Prints shell input lines as they are read.
- trap: Can be used to debug functions or specific parts of your script.

Example of using trap:

```
trap 'echo "Line $LINENO: Command \\"$BASH_COMMAND\\" exited with status $?"' ERR
```

## 5. Use a debugger

For more complex scripts, you might want to use a debugger. Bashdb is a popular bash script debugger. Here's how to use it:

a) Install bashdb (on Ubuntu/Debian):

`sudo apt-get install bashdb`

b) Run your script with bashdb:

`bashdb your_script.sh`

This will start an interactive debugging session where you can set breakpoints, step through the code, and inspect variables.

## 6. Check for syntax errors

Before diving into debugging, check for syntax errors:

`bash -n your_script.sh`

This will check for syntax errors without executing the script.

## 7. Use shellcheck

Shellcheck is a static analysis tool for shell scripts. It can catch common errors and suggest improvements:

a) Install shellcheck (on Ubuntu/Debian):

`sudo apt-get install shellcheck`

b) Run shellcheck on your script:

`shellcheck your_script.sh`

## 8. Debug specific sections

If you only want to debug a specific section of your script, you can use set -x and set +x to turn debugging on and off:

```
#!/bin/bash

# Normal execution
echo "This part is not debugged"

# Start debugging
set -x
echo "This part is debugged"
# Stop debugging
set +x

echo "Back to normal execution"
```

## 9. Use PS4 for more informative debug output

You can customize the prefix used for debug output using the PS4 variable:

```
export PS4='+(${BASH_SOURCE}:${LINENO}): ${FUNCNAME[0]:+${FUNCNAME[0]}(): }'
set -x

# Your script here
```

This will prefix each debug line with the source file, line number, and function name.

## 10. Check exit status

After each important command, check its exit status:

```
important_command
if [ $? -ne 0 ]; then
echo "Error: important_command failed"
exit 1
fi
```

## 11. Use bash's DEBUG trap

You can use the DEBUG trap to execute a command before each command in your script:

`trap 'echo "About to execute: $BASH_COMMAND"' DEBUG`

This will print each command before it's executed.

By combining these techniques, you can effectively debug your bash scripts and identify issues more quickly. Remember to remove or comment out debugging code before using the script in production.
