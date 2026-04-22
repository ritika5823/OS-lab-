```c
Name: Jash Chauhan
PRN: 24070521242
```

# Experiment 2: Process Management Commands

## Aim
To implement all process management commands. 

***

## Theory
In Linux, a process is a running instance of a program, identified by a unique Process ID (PID).  
Each process also has a Parent Process ID (PPID) indicating which process created it.  
Processes can run in foreground or background, and their priority can be adjusted using niceness values from -20 (highest) to 19 (lowest).

***

## Commands Reference

| Sr. No | Command              | Description                                      |
|--------|----------------------|--------------------------------------------------|
| 1      | `application &`      | Runs application in background                   |
| 2      | `pidof processname`  | Returns PID of running program                   |
| 3      | `fg job_no`          | Brings background job to foreground              |
| 4      | `top`                | Live view of system processes and resources      |
| 5      | `kill pid`           | Terminates process using PID                     |
| 6      | `nice -n [val] [name]` | Starts process with specific priority          |
| 7      | `ps`                 | Shows processes in current terminal              |
| 8      | `pstree`             | Displays parent-child process hierarchy          |
| 9      | `ps aux`             | All processes with user/CPU/Memory details       |
| 10     | `ps -axjk`           | Processes in hierarchical tree format            |
| 11     | `renice -n [val] [pid]` | Changes priority of running process           |
| 12     | `jobs`               | Shows active background/stopped jobs             |
| 13     | `bg`                 | Resumes suspended job in background              |
| 14     | `killall [name]`     | Kills all processes with given name              |
| 15     | `pkill [name]`       | Terminates processes by name matching            |

***

## Commands with Examples
```text
# 1. Run process in background
gedit &
# Output:  [delightlylinux.wordpress](https://delightlylinux.wordpress.com/2012/06/25/what-is-pid-and-ppid/) 4523

# 2. List background/stopped jobs
jobs
# Output:  [delightlylinux.wordpress](https://delightlylinux.wordpress.com/2012/06/25/what-is-pid-and-ppid/)+  Running    gedit &

# 3. Get PID of running process
pidof