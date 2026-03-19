# Linux Troubleshooting Drill (Docker)

> **Goal:** Build a repeatable, production-style troubleshooting routine covering CPU, memory, disk, network, and logs.

---

## Target Service

* **Service:** docker
* **Main process:** dockerd
* **Environment:** Ubuntu 24.04.1 LTS on WSL2

---

## 1. Environment Basics

### 1.1 Kernel & system info

```bash
uname -a
```

**Output / Screenshot:**

<img width="1541" height="564" alt="uname" src="https://github.com/user-attachments/assets/1ab2caf7-00c8-4f22-a5c7-10c50eea6a6c" />

---

### 1.2 OS details

```bash
lsb_release -a
```

```bash
cat /etc/os-release
```

**Notes:**

* Confirm OS version is supported and not EOL
* WSL2 kernel behaves differently from bare metal (important for IO & networking)

---

## 2. Filesystem Sanity Check

```bash
mkdir /tmp/runbook-demo
cp /etc/hosts /tmp/runbook-demo/hosts-copy-file
ls -l /tmp/runbook-demo
```

**Output / Screenshot:**

<img width="1099" height="172" alt="runbook-demo" src="https://github.com/user-attachments/assets/ef97bab7-e67f-4123-8a11-7fff0e29ca67" />


**Notes:**

* Confirms disk is writable
* Rules out basic filesystem or permission issues

---

## 3. CPU & Memory Snapshot

### 3.1 Overall system usage

```bash
top
```

**Output / Screenshot:**

<img width="1529" height="968" alt="top" src="https://github.com/user-attachments/assets/889dd814-427f-45e0-8520-11119285b79f" />

**What to check:**

* Load average
* dockerd CPU usage
* Idle CPU percentage

---

### 3.2 Process-level usage

```bash
ps aux | grep dockerd
ps -o pid,pcpu,pmem,comm -p $(pidof dockerd)
```

**Output / Screenshot:**

<img width="1272" height="183" alt="grep-docker" src="https://github.com/user-attachments/assets/6ffd0e11-8d86-4f6d-9659-8bcca681226d" />


**Notes:**

* Confirms which PID is dockerd
* Validates CPU & memory consumption

---

### 3.3 Memory availability

```bash
free -h
```

**Output / Screenshot:**

<img width="1002" height="153" alt="free-h" src="https://github.com/user-attachments/assets/4ad47a87-450d-4991-84e7-bf9c6a665214" />

**Notes:**

* Check available memory
* Ensure swap is not heavily used

---

## 4. Disk & IO Health

### 4.1 Disk usage

```bash
df -h
```

**Output / Screenshot:**

<img width="885" height="280" alt="df-h" src="https://github.com/user-attachments/assets/781a1463-7927-4b5e-a5a3-04726e1e87b6" />

**Notes:**

* Ignore snapfs 100% usage (expected)
* Focus on root filesystem and /var

---

### 4.2 Log directory size

```bash
sudo du -sh /var/log
```

**Output / Screenshot:**
<img width="993" height="144" alt="var-log" src="https://github.com/user-attachments/assets/d1169601-3aa1-4da6-ba86-52c3ecf04650" />

**Notes:**

* Large log growth can cause disk pressure
* Verify log rotation is working

---

### 4.3 IO statistics

```bash
iostat
vmstat 1
vmstat 1 5
dstat -cdnm
```

**Output / Screenshot:**

<img width="1234" height="467" alt="iostat" src="https://github.com/user-attachments/assets/98105e29-9aaf-4aea-a295-732799a8400d" />
<img width="1524" height="980" alt="vmstat" src="https://github.com/user-attachments/assets/84d86d6d-cd05-4317-bb41-dc7db6864e66" />
<img width="1199" height="275" alt="vmstat1-5" src="https://github.com/user-attachments/assets/b794970d-75f7-4d4c-94b9-f03f3f19c4bb" />

---

**Notes:**

* Check IO wait
* Ensure no swap-in or swap-out activity

---

## 5. Network Checks

### 5.1 Listening sockets

```bash
sudo ss -tulpn | grep docker
sudo ss -lx | grep docker
```

**Output / Screenshot:**

<img width="1272" height="183" alt="grep-docker" src="https://github.com/user-attachments/assets/3239f980-6ad2-4de7-b00c-f866e68510cb" />

**Notes:**

* Docker should listen only on Unix sockets
* No unexpected exposed TCP ports

---

### 5.2 Docker API health

```bash
curl --unix-socket /var/run/docker.sock http://localhost/_ping
```

**Expected:** `OK`

---

## 6. Log Analysis

### 6.1 Docker service logs

```bash
journalctl -u docker -n 50
```

**Output / Screenshot:**

<img width="1907" height="755" alt="journalctl" src="https://github.com/user-attachments/assets/cc00e8a8-4c1d-4880-9a1b-4c3f44679cbe" />

**Notes:**

* Look for crash loops or repeated restarts
* Warnings are acceptable if service is stable

---

## 7. Quick Findings

* System is healthy and mostly idle
* dockerd resource usage is minimal
* No CPU, memory, disk, or IO pressure
* Docker responding correctly to API checks
* Observed warnings are non-fatal

---

## 8. If This Worsens (Next Steps)

1. **Immediate containment**

```bash
systemctl restart docker
```

2. **Deeper diagnostics**

```bash
docker stats
dockerd --debug
```

3. **Advanced troubleshooting**

* Inspect container logs
* Capture `strace` on dockerd
* Review container restart behavior

---