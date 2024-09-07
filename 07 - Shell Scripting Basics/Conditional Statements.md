# Conditional Statements in Bash

Conditional statements in Bash allow you to control the flow of your script based on certain conditions. They enable your script to make decisions and execute different code blocks depending on whether specific conditions are true or false.

## 1. if statement

The most basic conditional statement is the 'if' statement. Its syntax is:

```
if [ condition ]; then
# commands to execute if condition is true
fi
```

Example:

```
#!/bin/bash

age=18

if [ $age -ge 18 ]; then
echo "You are an adult."
fi
```

## 2. if-else statement

The if-else statement allows you to specify actions for both when the condition is true and when it's false:

```
if [ condition ]; then
# commands to execute if condition is true
else
# commands to execute if condition is false
fi
```

Example:

```
#!/bin/bash

age=16

if [ $age -ge 18 ]; then
echo "You are an adult."
else
echo "You are a minor."
fi
```

## 3. if-elif-else statement

For multiple conditions, use the if-elif-else structure:

```
if [ condition1 ]; then
# commands for condition1
elif [ condition2 ]; then
# commands for condition2
elif [ condition3 ]; then
# commands for condition3
else
# commands if none of the conditions are true
fi
```

Example:

```
#!/bin/bash

grade=75

if [ $grade -ge 90 ]; then
echo "A"
elif [ $grade -ge 80 ]; then
echo "B"
elif [ $grade -ge 70 ]; then
echo "C"
elif [ $grade -ge 60 ]; then
echo "D"
else
echo "F"
fi
```

## 4. Comparison operators

Bash uses different operators for string and numeric comparisons:

Numeric comparisons:
- -eq: equal to
- -ne: not equal to
- -lt: less than
- -le: less than or equal to
- -gt: greater than
- -ge: greater than or equal to

String comparisons:
- =: equal to
- !=: not equal to
- <: less than (in ASCII alphabetical order)
- \>: greater than (in ASCII alphabetical order)
- -z: string is null (zero length)
- -n: string is not null

Example:

```
#!/bin/bash

num1=10
num2=20
str1="hello"
str2="world"

if [ $num1 -lt $num2 ]; then
echo "$num1 is less than $num2"
fi

if [ $str1 != $str2 ]; then
echo "$str1 is not equal to $str2"
fi
```

## 5. Logical operators

Bash supports logical AND and OR operations:

- &&: AND # Double ampersand Shift+7 (qwerty)
- ||: OR # Double Pipe | | with no spaces!

Example:

```
#!/bin/bash

age=25
has_license=true

if [ $age -ge 18 ] && [ "$has_license" = true ]; then
echo "You can drive a car."
fi

if [ $age -lt 18 ] || [ "$has_license" != true ]; then
echo "You cannot drive a car."
fi
```

## 6. Case statement

The case statement is useful when you have multiple conditions based on a single variable:

```
case $variable in
pattern1)
# commands for pattern1
;;
pattern2)
# commands for pattern2
;;
*) # This is the default or catch-all case
# default case
;;
esac
```

Example:

```
#!/bin/bash

fruit="apple"

case $fruit in
"apple")
echo "This is a red fruit."
;;
"banana")
echo "This is a yellow fruit."
;;
"grape")
    echo "This is a purple fruit."
;;
*)
echo "Unknown fruit."
;;
esac
```

## 7. Test command

The test command is often used in conditional statements. It's equivalent to using square brackets []. You can use it like this:

```
if test $a -eq $b; then
echo "a is equal to b"
fi
```

This is the same as:

```
if [ $a -eq $b ]; then
    echo "a is equal to b"
fi
```

## 8. Double square brackets

Bash also supports double square brackets [[ ]] for conditional tests. These provide more features than single brackets, such as pattern matching:

```
#!/bin/bash

string="Hello, World!"

if [[ $string == Hello* ]]; then
echo "String starts with 'Hello'"
fi
```

Double brackets also allow you to use && and || inside the condition:

```
if [[ $a -eq 5 && $b -gt 10 ]]; then
echo "Condition met"
fi
```