#  Networking Notes – DHCP, NTP & 3-Way Handshake

---

##  DHCP (Dynamic Host Configuration Protocol)

- DHCP gives **IP addresses automatically** to devices in a network.  
- No need to set IP manually.  
- Works on **UDP port 67 (Server)** and **UDP port 68 (Client)**.

###  Steps – DORA Process

1. **Discover** → Client sends message to find DHCP Server.  
2. **Offer** → Server offers an IP address.  
3. **Request** → Client asks to use that IP.  
4. **Acknowledge** → Server confirms and assigns IP.

Example:  
Client gets IP `192.168.1.10` automatically.

### 🧾 DHCP Gives:
- IP Address  
- Subnet Mask  
- Default Gateway  
- DNS Server  
- Lease Time

---

##  NTP (Network Time Protocol)

- NTP is used to **synchronize time** between all computers.  
- It works on **UDP port 123**.  
- It **does not use 3-way handshake** because it uses UDP.

###  How It Works:
1. Client sends request with its current time.  
2. Server replies with accurate time.  
3. Client adjusts its clock using the time difference.

Used for keeping all systems’ clocks the same.

---

## TCP 3-Way Handshake

- Used to **start a reliable connection** between two devices.  
- Works on **TCP (Transmission Control Protocol)**.

###  Steps:
1. **SYN** → Client: "Hello, I want to connect."  
2. **SYN-ACK** → Server: "Okay, I’m ready."  
3. **ACK** → Client: "Let’s start communication."

After this, data transfer begins.

---

## Summary Table

| Protocol | Use | Port | Type | Steps |
|-----------|-----|------|------|-------|
| **DHCP** | Gives IP automatically | UDP 67, 68 | Connectionless | DORA (4 steps) |
| **NTP** | Time synchronization | UDP 123 | Connectionless | Time exchange |
| **TCP (3-Way Handshake)** | Start connection | TCP | Connection-oriented | SYN → SYN-ACK → ACK |

---

**Tip:**  
Remember —  
- DHCP → IP auto assign  
- NTP → Time sync  
- TCP Handshake → Start connection

