# Network Troubleshooting Tools

Troubleshooting in networking means finding and fixing issues that stop devices from communicating. As B.Tech students, we often use basic tools to check connectivity, find delays, and verify whether services are running properly.

##  1. **ping**

**Purpose:**  
Used to check if another device or server is reachable over the network.

**How it works:**
When we use `ping`, our computer sends small test packets to the destination device. These packets are called **ICMP Echo Request** messages. If the other device is active and reachable, it responds with **ICMP Echo Reply**.

During this process:

- The packet first goes to the **default gateway (router)**.
- Then it travels through other routers in the network (if the destination is far).
- It finally reaches the target device.
- The target device sends a reply back the same way.

Ping measures:

- **Round-trip time** (time taken to send and receive data)
- **Packet loss** (how many packets didn't return)
- **TTL value** (shows how far the packet traveled)

If no reply comes back, it means:
- Device is offline OR
- Wrong IP address OR
- Network cable/wifi problem OR
- Firewall blocking ICMP

This simple test helps confirm if network connectivity exists or not

**Why we use it:**
- Test network connectivity  
- Check response time (latency)  
- Identify unstable network links  

**Example usage:**  
Typing `ping 8.8.8.8` in terminal checks internet connectivity by contacting Google DNS.

**Important terms:**
- **TTL** → Time-to-Live (number of hops allowed)  
- **Time** → Delay in milliseconds  

If there is no reply, it means network failure, device is off, wrong IP, or ICMP is blocked.

---

##  2. **traceroute / tracert** (Windows)

**Purpose:**  
Shows the route packets take from source to destination and finds where delay or failure occurs.

**How it works:**
raceroute helps us see **all the routers** a packet passes through before reaching the final destination.

It works using a concept called **TTL – Time To Live**:

- First packet is sent with TTL = 1  
  → It reaches first router and stops  
  → That router returns an error message and its IP address  

- Next packet TTL = 2  
  → Reaches Router 1 → Router 2 → stops  
  → We see 2nd router's IP  

This continues until the packet reaches the final destination or the route fails.

So traceroute shows:
- **Each hop (router)** on the path
- **Time taken at each hop**
- Where delay or packet loss happens

If traceroute hangs or star-marks (*) appear at some hop, it means:
- Router is overloaded OR
- Router is not responding to traceroute OR
- There is a network break at that hop

Traceroute is very useful to find **where exactly the network is failing**
**Why we use it:**
- Find path to a destination  
- Detect slow or failing network points  
- Troubleshoot routing issues  

**Example usage:**  
- `traceroute google.com` (Linux/Mac)  
- `tracert google.com` (Windows)  

If traceroute stops at a hop, that hop might be down, overloaded, or blocked.

---

##  3. **telnet**

**Purpose:**  
Checks if a specific network port is open and responding on a remote device.

> Telnet is not used for secure login today because it is not encrypted, but it is still useful for testing ports.

#### How it works (Detailed)
Telnet checks if a **specific port** on a remote device is open and responding.

Steps when you run telnet:

1. Your system tries to create a connection to a destination IP and port  
   (Example: `telnet 192.168.1.10 80` tests web port 80)

2. If the port is open, the remote machine answers the request  
   → You see a blank screen or connected message  
   → Means service on that port is running

3. If the port is closed or blocked:
   → Connection fails  
   → Means either firewall is blocking, or service is not running

Telnet does not encrypt data, so it is unsafe for login, but still very helpful for **port troubleshooting**.


**Why we use it:**
- Test whether a server port is reachable  
- Check firewall or service blocking  
- Useful for troubleshooting services like web servers and databases  

**Example usage:**  
Typing `telnet 192.168.1.10 80` tests if port 80 (web server) is running on that IP.

- If connection opens → **port working**  
- If connection fails → **port blocked or service down**

---

##  4. **SSH (Secure Shell)**

**Purpose:**  
Secure way to remotely login and manage network devices or servers.

**Difference from Telnet:**
- SSH is **encrypted and secure**  
- Telnet is **unencrypted and unsafe** for login

  #### How it works (Detailed)
SSH helps securely control another computer or network device remotely.

Here is what happens when we use SSH:

1. You type an SSH command like `ssh user@serverIP`
2. Your system sends an encrypted connection request
3. Both computers complete a **key exchange process**
   - They verify identity
   - They create a secure encrypted channel
4. You enter your password (or key authentication is used)
5. After successful login, you get a **remote terminal session**  
   (you control the remote machine like you are sitting there)

SSH uses **encryption**, meaning all data (username, password, commands) is secure from hackers.

It is commonly used by:
- Network engineers
- System admins
- DevOps and cloud engineers

**Why we use it:**
- Manage servers remotely  
- Configure network devices securely  
- Transfer files and execute commands safely  

**Example usage:**  
Typing `ssh username@192.168.1.10` connects securely to the device.

---

##  Table

| Tool | Purpose | Key Function | Common Use |
|------|--------|-------------|------------|
| **ping** | Check connectivity | Sends ICMP request & waits for reply | Test if device is reachable |
| **traceroute / tracert** | Show network path | Displays hops and delays | Find where network is slow or failing |
| **telnet** | Test specific port | Checks if port is open | Troubleshoot service/port issues |
| **SSH** | Secure remote login | Encrypted access to devices | Manage servers and network devices |

---

## ONE short Answer

In real-world and lab troubleshooting:

1. Start with **ping** to check connectivity  
2. Use **traceroute** to find path issues  
3. Use **telnet** to check services/ports  
4. Use **SSH** for secure remote access and administration  

