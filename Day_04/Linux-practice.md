# 📘 Day 04 – Linux Practice: Processes and Services

## 🎯 Objective

The objective of this task is to practice Linux fundamentals by working with real system commands.

In this task, I explored:

- Process management commands  
- Service management using systemctl  
- Log monitoring commands  
- Basic troubleshooting steps  

This hands-on practice helped me understand how Linux handles processes and services internally.

---

# 🔹 Process Management Commands

## 🔸 Command: ps aux

### 📂 Category: Process Management

```bash
ps aux
```
<img width="1468" height="985" alt="Screenshot 2026-02-14 155240" src="https://github.com/user-attachments/assets/15b8e899-f00f-4331-a24a-c1e71dd9d6fe" />


### ✅ Explanation

ps → Displays running processes

a → Shows processes for all users

u → Displays user-oriented format

x → Includes processes not attached to terminal

This command shows all currently running processes along with CPU, memory usage, and process IDs.



---


## 🔸 Command 2: top

### 📂 Category: Process Monitoring (Real-time)

```bash
top
```
<img width="1324" height="985" alt="Screenshot 2026-02-14 155318" src="https://github.com/user-attachments/assets/dc17c8b6-ffae-4cc0-a713-183ff7c228e6" />


### ✅ Explanation

- Displays real-time running processes  
- Shows CPU usage, memory usage, and load average  
- Helps identify high resource-consuming processes  

This command is useful for monitoring system performance live.

---



## 🔸 Command 3: pgrep ssh

### 📂 Category: Process Filtering

```bash
pgrep ssh
```
<img width="720" height="103" alt="Screenshot 2026-02-14 155356" src="https://github.com/user-attachments/assets/affb1670-e815-4aed-8038-db5a7e2a675f" />


### ✅ Explanation

- `pgrep` → Searches for processes by name  
- `ssh` → Process name  

This command returns the Process ID (PID) of the SSH service if it is running.

---


# 🔹 Service Management Commands

## 🔸 Command 4: systemctl status ssh

### 📂 Category: Service Management

```bash
systemctl status ssh
```

<img width="1903" height="562" alt="Screenshot 2026-02-14 155429" src="https://github.com/user-attachments/assets/7d2b4d49-bc3a-4c83-bf81-ae1ee58c69d8" />

### ✅ Explanation

- Shows whether SSH service is active or inactive  
- Displays service logs  
- Shows PID and uptime  

This helps verify if the SSH service is running properly.

---

## 🔸 Command 5: systemctl list-units --type=service

### 📂 Category: Service Listing

```bash
systemctl list-units --type=service
```

<img width="1786" height="973" alt="Screenshot 2026-02-14 155459" src="https://github.com/user-attachments/assets/7181e601-4f6a-48fe-96b0-06f0a4ebcac7" />

### ✅ Explanation

- Lists all active services in the system  
- Shows whether services are loaded, active, or running  

This helps understand what services are currently running.

---


# 🔹 Log Monitoring Commands

## 🔸 Command 6: journalctl -u ssh

### 📂 Category: Log Management

```bash
journalctl -u ssh
```

<img width="1889" height="975" alt="Screenshot 2026-02-14 155538" src="https://github.com/user-attachments/assets/cdfac7fb-b39d-489f-85d5-17494d0df119" />

### ✅ Explanation

- `journalctl` → Views system logs  
- `-u ssh` → Shows logs related to SSH service  

Useful for debugging service-related issues.

---


## 🔸 Command 7: tail -n 50 /var/log/syslog

### 📂 Category: Log Monitoring

```bash
tail -n 50 /var/log/syslog
```
<img width="1900" height="964" alt="Screenshot 2026-02-14 155615" src="https://github.com/user-attachments/assets/7026377e-80d4-47d6-999b-f087919eb50e" />

### ✅ Explanation

- `tail` → Shows last lines of a file  
- `-n 50` → Shows last 50 lines  
- `/var/log/syslog` → System log file  

This command is useful to check recent system activity and errors.

---

# 🔹 Mini Troubleshooting Example

## 🔸 Scenario: Restart SSH Service if Not Running

```bash
systemctl status ssh
```

<img width="1895" height="565" alt="Screenshot 2026-02-14 155654" src="https://github.com/user-attachments/assets/7346b0d6-8d33-4858-8cf7-fb1601f5b998" />

If the service is inactive:

```bash
sudo systemctl restart ssh
```


Verify again:

```bash
systemctl status ssh
```

### ✅ Explanation

- First check service status  
- Restart if inactive  
- Verify again  

This is a basic troubleshooting workflow for service issues.

---

# 🏁 Conclusion

In this practice session, I explored Linux process and service management commands.

I learned how to:

- Monitor running processes  
- Inspect system services  
- View logs  
- Perform basic troubleshooting  

This improved my understanding of Linux system internals and real-time monitoring.