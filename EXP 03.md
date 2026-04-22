```c
Name: Ritika Bhoyar
PRN: 24070521225
```

# Experiment 3: Fork and Exec System Calls

## Aim
To write a program to demonstrate process creating (Parent and Child).

***

## Theory
In Linux, `fork()` creates a new child process by duplicating the calling parent process, and both processes continue execution from the next statement after the call.
The `exec()` family replaces the current process image with a new program, so on success the old code does not continue after the `exec` call.
The `wait()` system call makes the parent pause until the child finishes, which helps collect the child’s exit status and prevents zombie processes.

***

## Formulae / Return Values
- `fork()` returns:
  - `> 0` → in parent process, value is child’s PID.
  - `= 0` → in child process.
  - `< 0` → fork failed.

- `exec()` returns:
  - Returns only on failure (`-1`).
  - On success, the current process is replaced and no return occurs.

***

## Compilation & Execution (Linux)

### 🔹 For 1_fork_1242.c
```bash
# Step 1: Create/Edit file
gedit 1_fork_1242.c

# Step 2: View code
cat 1_fork_1242.c

# Step 3: Compile
gcc 1_fork_1242.c -o 1_fork.out

# Step 4: Run
./1_fork.out
```

### 🔹 For 2_fork_1242.c
```bash
# Step 1: Create/Edit file
gedit 2_fork_1225.c

# Step 2: View code
cat 2_fork_1225.c

# Step 3: Compile
gcc 2_fork_1225.c -o 2_fork.out

# Step 4: Run
./2_fork.out
```

## Code - 1 FORK FUNCTION
```c
#include <unistd.h>
#include <stdio.h>

int main()
{
    int cpr;

    cpr = fork();

    if (cpr < 0)
    {
        printf("Fork failed to create process\n");
    }
    else if (cpr == 0)
    {
        // Child process
        printf("Process created\n");
        printf("Process id of the child process: %d\n", getpid());
        printf("Process id of the parent process: %d\n", getppid());
    }
    else
    {
        // Parent process
        printf("In parent process\n");
    }

    return 0;
}
```

## Code - 2 FORK FUNCTION
```c
#include <unistd.h>
#include <stdio.h>

int main()
{
    int f1, f2;

    f1 = fork();

    if (f1 < 0)
    {
        printf("First fork failed\n");
        return 1;
    }

    f2 = fork();

    if (f2 < 0)
    {
        printf("Second fork failed\n");
        return 1;
    }

    printf("Process ID: %d\n", getpid());
    printf("Parent Process ID: %d\n", getppid());
    printf("Hello from process\n\n");

    return 0;
}
```

## Output
```c
Output:

--- 1 FORK FUNCTION ---
In parent process
Process created
Process id of the child process: 6579
Process id of the parent process: 1929

[Parent] Child has finished execution.
[Parent] Continuing parent process...

--- 2 FORK FUNCTION ---
Process ID: 7546
Parent Process ID: 4031
Hello from process

Process ID: 7548
Parent Process ID: 7546
Hello from process

Process ID: 7547
Parent Process ID: 1929
Hello from process

Process ID: 7549
Parent Process ID: 7547
Hello from process
```
