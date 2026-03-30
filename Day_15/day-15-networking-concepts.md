# Day 15: Networking Concepts: DNS, IP, Subnets & Ports

---
## Task 1: **DNS:** How Names Become IPs.

**1. What happens when you type `google.com` in a browser?**

**Answer...**

When you enter a website in your browser, it first checks its cache for the IP address. If not found, it asks a DNS server to get the correct IP. Then your computer creates a secure HTTPS connection using TCP/IP with the server. The request goes through a load balancer to the correct web server, which processes it (sometimes using databases) and sends the webpage back to your browser.

**2. What are these record types? Write one line each:**

**Answer...**

- A Record – Connects a domain name to its IPv4 address.

- AAAA Record – Connects a domain name to its IPv6 address.

- CNAME Record – Points one domain name to another domain name (alias).

- MX Record – Tells which mail server handles emails for the domain.

- NS Record – Shows which name servers are responsible for the domain.

**3. Run: `dig google.com` identify the A record and TTL from the output**

<img width="903" height="568" alt="Screenshot 2026-03-30 195929" src="https://github.com/user-attachments/assets/d2283085-214e-456e-a7fd-e634994b76fa" />

* `A` - record gives IPv4 address - 142.250.67.174
* `TTL` - Time To Live - 46secs
---
## Task 2: IP Addressing...



### Task 2: IP Addressing
**1. What is an IPv4 address? How is it structured? (e.g., `192.168.1.10`)**

**Answer...**

An IPv4 address (Internet Protocol Version 4) is a unique numerical identifier assigned to every device connected to a network that uses the Internet Protocol for communication.

It helps devices locate and communicate with each other over a network.

### Structure of an IPv4 Address

An IPv4 address is divided into two main parts:
 1. Network Portion
 2. Host Portion

### Example

IP Address: `192.168.1.10`

- Network Portion: `192.168.1.0`
- Host Portion: `10`

**2. Difference between **public** and **private** IPs — give one example of each..?**

**Answer...**

### Difference Between Public IP and Private IP

| **Public IP Address** | **Private IP Address** |
|-----------------------|------------------------|
| A public IP address is assigned by an Internet Service Provider (ISP). | A private IP address is assigned within a local network (home, office, etc.). |
| It is globally unique and accessible over the internet. | It is not accessible directly from the internet. |
| It allows devices to communicate with external networks. | It is used for communication between devices inside the same network. |
| Example: `103.176.157.29`, `8.8.8.8 (Google DNS)` | Example: `192.168.x.x`, `10.x.x.x`, `172.16.x.x – 172.31.x.x` |


**3. What are the private IP ranges?**   
**- `10.x.x.x`, `172.16.x.x – 172.31.x.x`, `192.168.x.x`**

**Answer...**

# Private IP Address Ranges

Private IP addresses are reserved for use within local networks and are not routable on the public internet. Different ranges are used depending on the size and type of the network:

| **IP Range** | **Typical Usage** |
|--------------|------------------|
| `10.x.x.x` | Large enterprise networks |
| `172.16.x.x – 172.31.x.x` | Medium-sized organizations |
| `192.168.x.x` | Home networks and small offices |

> These IP addresses allow devices within the same network to communicate without exposing them directly to the internet.

4. Run: `ip addr show` — identify which of your IPs are private

<img width="1213" height="451" alt="Screenshot 2026-03-30 200002" src="https://github.com/user-attachments/assets/0fc71920-3c71-4060-91ef-085961e20e32" />

127.0.0.1/8 - Reserved for local host communication

192.168.100.133/24 - This is a private IP address.

---

## Task 3: CIDR & Subnetting

### 1. What does `/24` mean in `192.168.1.0/24`?

The `/24` is **CIDR (Classless Inter-Domain Routing) notation**. It indicates how many bits of the IP address are dedicated to the network part.  

- In this case, the first **24 bits** (out of 32) represent the network.  
- The remaining **8 bits** are used for hosts (individual devices) within that network.  

**IP range example:** `192.168.1.0 – 192.168.1.255`  
**Total IP addresses:** 256  



### 2. Number of usable hosts for common subnets

- `/24` → 254 usable hosts  
- `/16` → 65,534 usable hosts  
- `/28` → 14 usable hosts  

> Note: Two addresses in every subnet are reserved — one for the network and one for the broadcast address, which is why usable hosts are slightly fewer than total IPs.


### 3. Why subnet a network?

Subnetting is the process of splitting a large network into **smaller, manageable sections**. This brings multiple benefits:

- **Better performance:** Traffic stays within its subnet, reducing overall network congestion.  
- **Improved security:** Access can be restricted to specific subnets without exposing the entire network.  
- **Simpler management & troubleshooting:** Smaller networks are easier to monitor, maintain, and isolate problems.



### 4. Quick Reference Table

| CIDR | Subnet Mask       | Total IPs | Usable Hosts |
|------|-----------------|-----------|--------------|
| /24  | 255.255.255.0   | 256       | 254          |
| /16  | 255.255.0.0     | 65,536    | 65,534       |
| /28  | 255.255.255.240 | 16        | 14           |

---

# Task 4: Ports – The Doors to Services

### 1. What is a port and why do we need it?

A **port** is a logical channel used in networking to direct data to the correct service on a device.  

- The **IP address** identifies the device on the network.  
- The **port number** identifies the specific service or application running on that device.  
- Ports are necessary to allow multiple services to run on the same machine without conflicts.



### 2. Common Ports and Their Services

| Port | Service |
|------|---------|
| 22   | SSH     |
| 80   | HTTP / Nginx |
| 443  | HTTPS   |
| 53   | DNS     |
| 3306 | MySQL   |
| 6379 | Redis   |
| 27017| MongoDB |

---

### 3. Checking Listening Ports

Run the command:

```
ss -tulpn
```
Example mapping:
```
Port 22 → SSH service

Port 80 → Apache2 / Nginx service
```
---


## Task 5: Putting It All Together

Example 1: Accessing a web service

Command:
```
curl http://localhost:80
```
Breakdown:

- Protocol: HTTP

- Localhost: Resolves to loopback IP 127.0.0.1

- Port 80: Apache or Nginx service handling the request


- Your app can't reach a database at `10.0.1.50:3306` — what would you check first?
   * `ss -tulpn | grep 3306` - Check if port is open and service is listening.
   * `systemctl status mysql` - Check service status
   * `nc -zv 10.0.1.50 3306` - Check connectivity
   * `journalctl -u mysql` - Check Logs