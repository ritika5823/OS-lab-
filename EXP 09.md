```c
Name: Ritika Bhoyar
PRN: 24070521225
```

# Experiment 9: Basic Shell Commands and Shell Script - Arithmetic

## Aim
To implement basic shell commands and write a shell script to perform arithmetic operations.

***

## Theory
A shell script is a text file containing a sequence of shell commands.  
The shebang line `#!/bin/bash` tells the system which interpreter to use for execution.  
Bash supports arithmetic using `$(( ))` syntax, and variables are assigned without spaces using `var=value`. 

***

## Basic Commands
- `touch <file>` - creates an empty file
- `chmod 777 <file>` - gives read, write, and execute permission to all
- `sudo chown <user>` - changes file ownership
- `echo "text" > file` - writes text to a file and overwrites existing content
- `cat <file>` - displays file content
- `grep <pattern>` - searches for a pattern in a file
- `find . -name` - searches for files by name
- `df -h` - shows disk space usage in human readable form
- `free -h` - shows RAM and swap usage in human readable form
- `ping <host>` - tests network connectivity

***

## Compilation & Execution (Linux):
```c
Step 1: Create file using vim or gedit
         gedit arith_1225.sh

Step 2: Make the script executable
         chmod +x arith_1225.sh

Step 3: Run the script
         ./arith_1225.sh
```

## Code
```bash
#!/bin/bash

echo "Enter first number"
read a

echo "Enter second number"
read b

c=$(( a + b ))
echo "Addition is $c"

d=$(( a - b ))
echo "Subtraction is $d"

e=$(( a * b ))
echo "Multiplication is $e"

f=$(( a % b ))
echo "Remainder is $f"

g=$(( a / b ))
echo "Quotient is $g"
```

## Output
```c
Output:
Enter first number
10
Enter second number
5
Addition is 15
Subtraction is 5
Multiplication is 50
Remainder is 0
Quotient is 2
```
