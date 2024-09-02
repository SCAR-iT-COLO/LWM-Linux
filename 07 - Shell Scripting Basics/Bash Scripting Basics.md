# Introduction to Bash Scripting

Bash (Bourne Again SHell) is a command-line interface and scripting language used in Unix and Unix-like operating systems, including Linux and macOS. Bash scripts are text files containing a series of commands that can be executed by the Bash shell.

## 1. Creating a Bash Script

To create a Bash script:

- Open a text editor
- Start the file with a shebang: #!/bin/bash
- Add your commands
- Save the file with a .sh extension (e.g., myscript.sh)
- Make the script executable: chmod +x myscript.sh

Here's a simple example:

```bash
#!/bin/bash
echo "Hello, World!"
```

## 2. Variables

Variables in Bash are created by assigning a value:

```bash
name="John"
age=30
echo "Name: $name, Age: $age"
```

Use `$` to reference variables. For command substitution, use `$(command)`:

```bash
current_date=$(date +%Y-%m-%d)
echo "Today is $current_date"
```

## 3. User Input

Use `read` to get user input:

```bash
echo "What's your name?"
read user_name
echo "Hello, $user_name!"
```

## 4. Conditional Statements

If-else statements:

```bash
if [ "$age" -ge 18 ]; then
    echo "You are an adult"
else
    echo "You are a minor"
fi
```

Note the spaces around the brackets and comparison operator.

## 5. Loops

For loop:

```bash
for i in {1..5}
do
    echo "Iteration $i"
done
```

While loop:

```bash
counter=1
while [ $counter -le 5 ]
do
    echo "Counter: $counter"
    ((counter++))
done
```

## 6. Functions

Define and call functions:

```bash
greet() {
    echo "Hello, $1!"
}

greet "Alice"
greet "Bob"
```

## 7. Command-line Arguments

Access command-line arguments using `$1`, `$2`, etc.:

```bash
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"
```

## 8. File Operations

Check if a file exists:

```bash
if [ -f "myfile.txt" ]; then
    echo "myfile.txt exists"
else
    echo "myfile.txt does not exist"
fi
```

Read from a file:

```bash
while IFS= read -r line
do
    echo "$line"
done < "myfile.txt"
```
