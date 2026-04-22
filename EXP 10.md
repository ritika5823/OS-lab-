```c
Name: Jash Chauhan
PRN: 24070521242
```

# Experiment 10: Shell Script - if-else Conditional Statement

## Aim
To write a shell script to demonstrate if-else conditional statements by calculating student grade based on marks.

***

## Theory
Conditional statements in bash allow decision-making based on conditions.  
The `if`, `elif`, and `else` keywords are used to check different conditions and execute the matching block.  
Comparison operators like `-eq`, `-ne`, `-gt`, `-lt`, `-ge`, and `-le` are used for integer comparisons in bash.

***

## Formulae
- Total Marks = OS + EM3 + DS
- Percentage = Total Marks / 3

***

## Compilation & Execution (Linux):
```c
Step 1: Create file using nano or gedit
         nano exp10_1242.sh

Step 2: Make the script executable
         chmod +x exp10_1242.sh

Step 3: Run the script
         ./exp10_1242.sh
```

## Code
```bash
#!/bin/bash

echo "Enter OS marks:"
read os

echo "Enter EM3 marks:"
read em3

echo "Enter DS marks:"
read ds

total=$(( os + em3 + ds ))
echo "Total marks = $total"

percentage=$(( total / 3 ))
echo "Percentage = $percentage"

if [ $percentage -ge 75 ]
then
    echo "PASS with DISTINCTION"
elif [ $percentage -ge 60 ] && [ $percentage -le 74 ]
then
    echo "PASS with FIRST CLASS"
elif [ $percentage -ge 45 ] && [ $percentage -le 59 ]
then
    echo "PASS"
else
    echo "FAIL"
fi
```

## Output
```c
Output:
Enter OS marks: 70
Enter EM3 marks: 80
Enter DS marks: 75
Total marks = 225
Percentage = 75
PASS with DISTINCTION
```