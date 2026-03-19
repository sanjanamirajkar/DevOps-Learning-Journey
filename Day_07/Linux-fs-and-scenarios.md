# Day 07 – Linux File System Hierarchy & Scenario-Based Practice

Today's goal is to **understand the Linux file system structure** and **practice troubleshooting like a DevOps engineer**.  
We will explore important directories and solve scenario-based exercises to build hands-on troubleshooting skills.

---

## Part 1: Linux File System Hierarchy

| Directory | Purpose | Example Command | Observation / Note |
|-----------|--------|----------------|------------------|
| `/` | Root directory; starting point of the entire filesystem | `ls -l /` | Lists core directories like `bin`, `etc`, `home` |
| `/home` | User home directories | `ls -la /home` | Shows directories for users like `ubuntu`, `john` |
| `/root` | Root user's home directory | `ls -la /root` | Only accessible by root; contains root-specific configs |
| `/etc` | System configuration files | `ls -l /etc` | Contains `hostname`, `passwd`, `network` configs |
| `/var/log` | Log files, important for monitoring | `du -sh /var/log/* 2>/dev/null | sort -h | tail -5` | Shows largest log files for monitoring |
| `/tmp` | Temporary files | `ls -la /tmp` | Stores temporary files, cleared on reboot |
| `/bin` | Essential binaries for all users | `ls /bin | head -5` | Commands like `ls`, `cp`, `mv` |
| `/usr/bin` | User command binaries | `ls /usr/bin | head -5` | Additional commands and utilities installed by system |
| `/opt` | Optional / third-party applications | `ls /opt` | Often empty unless software installed here |


---

## Part 2: Scenario-Based Practice

### SOLVED EXAMPLE: Check if a service is running

**Question:** How do you check if the `nginx` service is running?

**Step 1:** Check service status
```
systemctl status nginx
```
Why: Displays whether the service is active, stopped, or failed.

**Step 2:** If service is not found, list all services
```
systemctl list-units --type=service
```
Why: Lists all services on the system to see what is available.

**Step 3:** Check if service is enabled on boot
```
systemctl is-enabled nginx
```
Why: Confirms whether the service will start automatically after a reboot.

**What I learned: Always start by checking the service status, then investigate further based on observations.**

## Scenario 1: Service Not Starting
**Problem:** A web application service myapp failed to start after a server reboot.

**Step 1:** Check service status
```
systemctl status myapp
```
Why: Verifies if the service is running, failed, or inactive.

**Step 2:** Review recent service logs
```
journalctl -u myapp -n 50
```
Why: Displays the last 50 lines of logs to understand why the service failed.

**Step 3:** Check if service is enabled on boot
```
systemctl is-enabled myapp
```
Why: Confirms whether the service is configured to start automatically on reboot.

**Step 4:** Restart the service if needed
```
systemctl restart myapp
```
Why: Attempts to fix the service after analyzing logs and configuration.

## Scenario 2: High CPU Usage
**Problem:** Application server is slow.

**Step 1:** Monitor live CPU usage
```
top
```
Why: Shows real-time CPU and memory usage of all processes.

**Step 2:** Use interactive process viewer
```
htop
```
Why: Easier to identify top CPU-consuming processes interactively.

**Step 3:** List top CPU processes
```
ps aux --sort=-%cpu | head -10
```
Why: Displays the top 10 processes by CPU usage to identify resource-heavy processes.

## Scenario 3: Finding Service Logs
** Problem:** Developer asks where logs for the docker service are.

**Step 1:** Check service status
```
systemctl status docker
```
Why: Confirms if the service is running and shows recent activity.

**Step 2:** View last 50 log entries
```
journalctl -u docker -n 50
```
Why: Quickly inspects recent service events for troubleshooting.

**Step 3:** Follow logs in real-time
```
journalctl -u docker -f
```
Why: Continuously monitors logs as events occur, similar to tail -f.

## Scenario 4: File Permissions Issue
**Problem:** Script /home/user/backup.sh cannot execute, gives Permission denied.

**Step 1:** Check current permissions
```
ls -l /home/user/backup.sh
```
Why: Shows file permissions; notice if execute (x) permission is missing.

**Step 2:** Add execute permission
```
chmod +x /home/user/backup.sh
```
Why: Grants execute rights so the script can run.

**Step 3** Verify permissions updated
```
ls -l /home/user/backup.sh
```
Why: Confirms the file now has x permission (-rwxr-xr-x).

**Step 4:** Execute the script
```
./backup.sh
```
Why: Runs the script successfully after fixing permissions.


## Key away Learnings points

- Always check service status first before troubleshooting further.
- Logs are the most important source of information (journalctl) for services.
- Monitoring CPU and memory helps identify performance bottlenecks.
- File execution issues are often due to missing x permission; chmod +x fixes it.
- Step-by-step approach avoids guesswork during incidents.