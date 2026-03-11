# 90 Days of DevOps – Day 02
## Linux Architecture and Processes

### 1. Core Components of Linux

**Kernel**
- Kernel is the core of the Linux operating system.
- It manages hardware resources like CPU, memory, disk, and network.
- It handles process scheduling, memory management, and device drivers.

**User Space**
- User space is where users and applications run.
- Commands, applications, and services work in user space.
- User space cannot directly access hardware; it communicates with the kernel.

**init / systemd**
- systemd is the first process started by the kernel (PID 1).
- It manages system startup, services, and background processes.
- It ensures services start in the correct order and stay running.

---

### 2. Linux Processes

A **process** is a running instance of a program.

**Process Creation**
- Processes are created using `fork()` and `exec()`.
- Every process has a unique Process ID (PID).
- Parent processes can create child processes.

**Process States**
- **Running** – Process is currently executing on CPU.
- **Sleeping** – Process is waiting for resources or input.
- **Stopped** – Process execution is paused.
- **Zombie** – Process has finished execution but still exists in process table.

---

### 3. systemd and Why It Matters

- systemd is the modern init system used by most Linux distributions.
- It manages services, system startup, logging, and service monitoring.
- It automatically restarts failed services.
- It helps DevOps engineers manage applications reliably in production.

Common systemd tasks:
- Start and stop services
- Check service status
- Enable services at boot
- View service logs

---

### 4. Daily Useful Linux Commands

1. `ps` – View running processes  
2. `top` – Monitor CPU and memory usage in real time  
3. `systemctl status service-name` – Check service status  
4. `systemctl start/stop service-name` – Manage services  
5. `journalctl` – View system and service logs

---

 ### 5. Why This Matters for DevOps

- Linux is the base OS for most production systems.
- Understanding processes and systemd helps in:
  - Debugging crashed services
  - Fixing CPU and memory issues
  - Analyzing logs during incidents
- This knowledge saves time and improves confidence in real-world troubleshooting.