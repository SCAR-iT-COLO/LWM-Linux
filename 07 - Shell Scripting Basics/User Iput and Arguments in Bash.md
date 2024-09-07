# User Input and Arguments in Bash

## 1. Command-line Arguments

Bash scripts can accept arguments when executed from the command line. These arguments are accessible within the script using special variables.

Example:

```
#!/bin/bash

echo "The script name is: $0"
echo "The first argument is: $1"
echo "The second argument is: $2"
echo "All arguments: $@"
```

Usage:
`./script.sh arg1 arg2 arg3`

## 2. The `read` Command

The `read` command allows interactive user input during script execution.

Basic syntax:
```
read variable_name
```

Example:

```
#!/bin/bash

echo "What's your name?"
read name
echo "Hello, $name!"

# Reading multiple variables
echo "Enter your first and last name:"
read first_name last_name
echo "Your full name is $first_name $last_name"

# Using a prompt
read -p "Enter your age: " age
echo "You are $age years old"

# Reading with a timeout
read -t 5 -p "Quick! Enter a number: " number
echo "You entered: $number"
```

## 3. Special Variables for Arguments

Bash provides special variables for working with command-line arguments:

- `$0`: Script name
- `$1`, `$2`, `$3`, etc.: Individual arguments
- `$#`: Number of arguments
- `$@`: All arguments as separate words
- `$*`: All arguments as a single word

Example:

```
#!/bin/bash

echo "Number of arguments: $#"
echo "All arguments: $@"

# Loop through all arguments
for arg in "$@"
do
    echo "Argument: $arg"
done
```

## 4. Handling Options and Flags

You can create scripts that accept options (flags) to modify behavior.

Example:

```
#!/bin/bash

verbose=false

while [[ $# -gt 0 ]]
do
key="$1"
case $key in
-v|--verbose)
verbose=true
shift
;;
-n|--name)
name="$2"
shift
shift
;;
*)
echo "Unknown option: $1"
exit 1
;;
esac
done

if [ "$verbose" = true ] ; then
echo "Verbose mode on"
fi

if [ ! -z "$name" ] ; then
echo "Hello, $name!"
fi
```

Usage:
`./script.sh -v --name John`

## 5. Validating Input

It's important to validate user input to ensure your script behaves correctly.

Example:

```
#!/bin/bash

read -p "Enter a number between 1 and 10: " number

if [[ ! $number =~ ^[0-9]+$ ]] ; then
echo "Error: Not a number"
exit 1
fi

if (( number < 1 || number > 10 )) ; then
echo "Error: Number out of range"
exit 1
fi

echo "You entered a valid number: $number"
```

## 6. Using `getopts` for Advanced Option Parsing

For more complex option parsing, Bash provides the `getopts` built-in command.

Example:

```
#!/bin/bash

usage() {
echo "Usage: $0 [-h] [-v] [-n name]"
echo "  -h: Display this help message"
echo "  -v: Enable verbose mode"
echo "  -n name: Specify a name"
}

verbose=false
name=""

while getopts ":hvn:" opt; do
case ${opt} in
h )
usage
exit 0
;;
v )
verbose=true
;;
n )
name=$OPTARG
;;
\? )
echo "Invalid option: $OPTARG" 1>&2
usage
exit 1
;;
: )
echo "Invalid option: $OPTARG requires an argument" 1>&2
usage
exit 1
;;
esac
done

if [ "$verbose" = true ] ; then
echo "Verbose mode enabled"
fi

if [ ! -z "$name" ] ; then
echo "Hello, $name!"
fi
```

Usage:
`./script.sh -v -n Alice`
