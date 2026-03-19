# Linux Commands 
### A practical Linux command reference focused on Process management,
### File system operations, and Network troubleshooting.

---

## 🔹 Process Management

| Command | Explanation |
|---------|------------|
| ps aux | Shows all running processes with CPU and memory usage |
| top | Displays real-time process activity |
| htop | Interactive and improved version of top (if installed) |
| pstree | Shows process hierarchy in tree format |
| kill <PID> | Gracefully stops a process |
| kill -9 <PID> | Forcefully terminates a process |
| pkill <name> | Kills process by name |
| nice -n 10 cmd | Starts process with lower CPU priority |
| renice -n 5 <PID> | Changes priority of running process |
| bg | Resumes a stopped job in background |
| fg | Brings background job to foreground |
| jobs | Lists active background jobs |
| nohup cmd & | Runs command in background after logout |

---

## 🔹 File System

| Command | Explanation |
|---------|------------|
| ls -la | Lists all files including hidden files |
| pwd | Shows current directory path |
| cd <dir> | Changes directory |
| mkdir <name> | Creates new directory |
| rm -rf <dir> | Deletes directory forcefully |
| cp -r src dest | Copies files/directories |
| mv src dest | Moves or renames files |
| touch file.txt | Creates empty file |
| cat file.txt | Displays file content |
| chmod 755 file | Changes file permissions |
| chown user:group file | Changes file ownership |
| find / -name file | Searches file by name |
| grep "word" file | Searches text inside file |

---

## 🔹 Networking

| Command | Explanation |
|---------|------------|
| ping google.com | Checks network connectivity |
| ip addr | Shows IP address details |
| curl https://example.com | Fetches data from URL |
| netstat -tulnp | Shows open ports and listening services |
| ss -tulnp | Displays socket statistics |
| dig google.com | DNS lookup information |