```c
Name: Jash Chauhan
PRN: 24070521242
```

# Experiment 1: Basic Linux Commands

## Aim
To implement basic Linux commands on Ubuntu.
---

## Theory
Linux is a Unix-based operating system. All interactions happen through the terminal using commands. The file system is organized as a tree starting from the root `/`. Every file and directory has permissions (read, write, execute) assigned to the owner, group, and others.

Key concepts:
- **Shell**: The command interpreter (e.g., bash) that reads and executes commands.
- **Directory**: A folder that contains files or other directories.
- **Path**: The location of a file or directory. Absolute paths start with `/`; relative paths start from the current directory.
- **Permissions**: Each file has read (r), write (w), and execute (x) permissions for owner, group, and others.

---

## Commands Reference

### Navigation & File Management

| Command | Description |
|---|---|
| `pwd` | Print the current working directory |
| `ls` | List files in current directory |
| `ls -la` | List all files including hidden, with permissions |
| `cd <path>` | Change directory to specified path |
| `mkdir <name>` | Create a new directory |
| `touch <file>` | Create an empty file |
| `cp <src> <dest>` | Copy file or folder |
| `mv <src> <dest>` | Move or rename a file/directory |
| `rm <file>` | Remove a file |
| `rm -rf <path>` | Remove directory and its contents recursively |

### File Operations

| Command | Description |
|---|---|
| `cat <file>` | Print file contents to terminal |
| `grep "pattern" <file>` | Search for a text pattern in a file |
| `nano <file>` | Open file in nano text editor |
| `vi <file>` | Open file in vi text editor |
| `tail -f <file>` | Show last lines of file, update live |

### Permissions & System

| Command | Description |
|---|---|
| `chmod 755 <file>` | Set read/write/execute permissions |
| `chown user:group <file>` | Change file ownership |
| `sudo <command>` | Run command with root/admin privileges |
| `df -h` | Show disk usage in human-readable format |
| `top` | Live view of system processes and resource usage |

---

## Commands with Examples

```bash
# 1. Print current working directory
pwd
# Output: /home/user

# 2. List files in current directory
ls
# Output: Desktop  Documents  Downloads  Music  Pictures

# 3. List all files including hidden, with permissions
ls -la
# Output:
# drwxr-xr-x  2 user user 4096 Jan 01 10:00 Desktop
# -rw-r--r--  1 user user  220 Jan 01 09:00 .bashrc

# 4. Create a new directory
mkdir myFolder
# Output: (no output, directory created)

# 5. Change to that directory
cd myFolder
# Output: (no output, directory changed)

# 6. Create an empty file
touch myFile.txt
# Output: (no output, file created)

# 7. Write text into file using echo
echo "Hello Linux" > myFile.txt

# 8. Print file contents
cat myFile.txt
# Output: Hello Linux

# 9. Copy file to another location
cp myFile.txt myFile_backup.txt

# 10. Rename a file using mv
mv myFile_backup.txt renamed.txt

# 11. Search for text in a file
grep "Hello" myFile.txt
# Output: Hello Linux

# 12. Check disk usage
df -h
# Output:
# Filesystem      Size  Used Avail Use% Mounted on
# /dev/sda1        50G   15G   33G  31% /

# 13. Set file permissions (rwxr-xr-x)
chmod 755 myFile.txt

# 14. Remove a file
rm renamed.txt

# 15. Go back to parent directory
cd ..

# 16. Remove the directory and all its contents
rm -rf myFolder
```

---

## Output
```
Output:

$ pwd
/home/user/Desktop

$ mkdir myFolder

$ cd myFolder

$ touch myFile.txt

$ echo "Hello Linux" > myFile.txt

$ cat myFile.txt
Hello Linux

$ cp myFile.txt myFile_backup.txt

$ mv myFile_backup.txt renamed.txt

$ ls -la
total 16
drwxr-xr-x 2 user user 4096 Jan 01 10:05 .
drwxr-xr-x 5 user user 4096 Jan 01 10:00 ..
-rw-r--r-- 1 user user   12 Jan 01 10:03 myFile.txt
-rw-r--r-- 1 user user   12 Jan 01 10:04 renamed.txt

$ grep "Hello" myFile.txt
Hello Linux

$ chmod 755 myFile.txt

$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   15G   33G  31% /

$ rm renamed.txt

$ cd ..

$ rm -rf myFolder
```