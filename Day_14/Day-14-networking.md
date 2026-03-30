# Day 14 Networking Fundamentals & Practical Verification..

## OSI Model & TCP/IP Model

### OSI Model (7 Layers)

The OSI (Open Systems Interconnection) model is a conceptual framework that explains how data travels across a network. It consists of seven layers, each responsible for a specific task.

- **Layer 7** – Application: Interface for end users (e.g., web browsers).

- **Layer 6** – Presentation: Handles encryption, decryption, and data formatting.

- **Layer 5** – Session: Manages session establishment and termination.

- **Layer 4** – Transport: Ensures reliable or fast delivery (TCP/UDP).

- **Layer 3** – Network: Handles IP addressing and routing.

- **Layer 2** – Data Link: Provides node-to-node communication.

- **Layer 1** – Physical: Physical hardware such as cables and signals.

### TCP/IP Model (Practical Model)

The TCP/IP model is the real-world networking model used on the internet.

- **Application Layer:** Combines OSI’s Application, Presentation, and Session layers.

- **Transport Layer:** Same role as OSI Transport (TCP/UDP).

- **Internet Layer:** Equivalent to OSI Network layer (IP routing).

- **Network Access Layer:** Combines Physical + Data Link layers.

### Protocol Layer Mapping

- **Application Layer:** HTTP, HTTPS, FTP, SMTP, DNS, DHCP, SSH

- **Transport Layer:** TCP, UDP

- **Internet Layer:** IP, ICMP, ARP

- **Network Access Layer:** Ethernet, Wi-Fi

**Real-World Example**
```
HTTP communication flow:

HTTP (Application)
   ↓
TCP (Transport)
   ↓
IP (Internet)
   ↓
Ethernet/Wi-Fi (Network Access)
```
Example command:
```
curl http://example.com

```

<img width="1911" height="432" alt="Screenshot 2026-03-19 201859" src="https://github.com/user-attachments/assets/6245fd32-3226-48e8-a0b6-0557e8e9f398" />

## Hands-on Networking Checks

Below are essential commands used to verify network connectivity and troubleshoot issues.

### Task 1: Check IP Address
```
hostname -I
```
<img width="1183" height="342" alt="Screenshot 2026-03-19 202111" src="https://github.com/user-attachments/assets/9ae9a8c9-ebdd-4db2-8572-d78103075886" />

**Observation:** Displays the system’s private/local IP address.

### Task 2: Test Connectivity
```
ping <target>
```
<img width="1183" height="342" alt="Screenshot 2026-03-19 202111" src="https://github.com/user-attachments/assets/2b64bcef-5f0c-4605-9859-c655ba496709" />

**Explain:**

- 0% packet loss → Network reachable

- High latency → Possible delay in routing

### Task 3: Trace Network Path
```
traceroute <target>
```
**Observation:**
Shows hop-by-hop path and identifies where delay occurs.

### Task 4: Check Open Ports
```
ss -tulpn
```
### or
```
netstat -tulpn
```
**Observation:**
Displays active services and listening ports (e.g., SSH on port 22).

Task 5: DNS Resolution
```
dig <domain>
# or
nslookup <domain>
```
<img width="1024" height="540" alt="Screenshot 2026-03-19 202153" src="https://github.com/user-attachments/assets/1a67f007-5cd4-42a2-bbf8-e625ef8ff3c9" />

**Observation:**
Confirms whether the domain resolves to a valid IP address.

Task 6: HTTP Response Test
```
curl -I http://<url>
```
**Observation:**

- 200 OK → Server responding properly

- 500 → Application issue

404 → Resource not found

Task 7: View Active Connections
```
netstat -an | head
```
**Observation:**
Shows LISTEN and ESTABLISHED connections.

## Mini Task: Port Testing

### Check SSH Port
```
ss -tulpn | grep 22
```
Test Port Connectivity
```
nc -zv <server-ip> 22
```

If connection fails:
```  
systemctl status ssh
journalctl -u ssh
sudo ufw status
```

## Troubleshooting Reflection...

### Ping Works → Network Layer is OK

If ping fails, start troubleshooting from Layer 3 (IP).

### DNS Fails → Check Application → Transport → Internet

Use:
```
dig
nslookup
ss -tulpn
```
<img width="1812" height="361" alt="Screenshot 2026-03-19 202236" src="https://github.com/user-attachments/assets/9f621be8-30f3-4d9e-95fe-b284d9dcb032" />

### HTTP 500 Error → Application Layer Issue

Since you received a response, Transport and Internet layers are working.
Check:
```
systemctl status <service>
journalctl -u <service>
tail -f /var/log/<service>/error.log
```

### Incident Follow-Up Checklist

- **Firewall status**
```
sudo ufw status
sudo iptables -L -n -v
```

- **Service health**
```
systemctl status <service>
```

- **Port connectivity**
```
curl -I http://<server-ip>:<port>
nc -zv <server-ip> <port>
```
<img width="926" height="118" alt="Screenshot 2026-03-19 202359" src="https://github.com/user-attachments/assets/d00be809-329d-481a-b69e-56003992270a" />

---

## **Final Summary......**

Understanding OSI and TCP/IP models helps identify where issues occur.
Using basic Linux networking commands allows quick diagnosis during real-world incidents.

Layer-by-layer troubleshooting saves time and makes debugging structured and efficient.