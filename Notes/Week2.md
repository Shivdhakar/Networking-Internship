# OSI Model Notes

The **OSI Model** is like a guide for how network devices communicate with each other.  
It divides the communication process into **7 layers**, where each layer performs a specific task to send data smoothly from one device to another.

---

##  The 7 Layers

### **Layer 1: Physical**  
This layer is all about hardware like cables, plugs, and signals.  
It sends **raw bits (0s and 1s)** through electrical, radio, or light signals.  
**Examples:** Ethernet cables, Hubs.

---

### **Layer 2: Data Link**  
Ensures data moves **error-free** between two directly connected devices.  
It uses **MAC addresses** and manages **frames**.  
**Examples:** Switches, Bridges.

---

### **Layer 3: Network**  
Handles **IP addresses** and finds the **best path** for data packets across networks.  
**Examples:** Routers, IPv4, IPv6.

---

### **Layer 4: Transport**  
Manages **data delivery** — either reliable (TCP) or fast (UDP).  
Handles **error checking, flow control**, and splits data into segments.  
**Examples:** TCP, UDP.

---

### **Layer 5: Session**  
Creates, manages, and ends connections between applications.  
Keeps communication organized between two devices.  
**Examples:** API sessions, RPC calls.

---

### **Layer 6: Presentation**  
Translates data formats for apps and networks.  
Handles **encryption, decryption, compression**.  
**Examples:** SSL, TLS, JPEG, MP3.

---

### **Layer 7: Application**  
The top layer — where users interact directly.  
Used for **web browsing, emails, file transfers**, etc.  
**Examples:** HTTP, FTP, SMTP, DNS.

---
 

# [Click here to view image osi model](../Asset/osi.png)


---

##  Summary Table

| Layer | Name | Function | Examples |
|-------|------|-----------|-----------|
| 7 | Application | User interaction | HTTP, FTP, SMTP, DNS |
| 6 | Presentation | Format, encrypt, compress | SSL, TLS, JPEG, MP3 |
| 5 | Session | Manage sessions | APIs, RPC |
| 4 | Transport | Reliable or fast data delivery | TCP, UDP |
| 3 | Network | Routing and addressing | IP, Routers |
| 2 | Data Link | Frames, MAC addressing | Switches, Bridges |
| 1 | Physical | Send bits through hardware | Ethernet, Hubs |

---

##  Example: WhatsApp Voice Call (VoIP)

When making a WhatsApp call, your **voice becomes data** that travels through all seven layers.

- **Layer 7 (Application):** WhatsApp starts the call and shows the interface.  
- **Layer 6 (Presentation):** Voice compressed using Opus codec and encrypted.  
- **Layer 5 (Session):** Maintains call session and syncs both users.  
- **Layer 4 (Transport):** Uses UDP for quick, real-time delivery.  
- **Layer 3 (Network):** Adds IP addresses and routes data.  
- **Layer 2 (Data Link):** Uses MAC for local network communication.  
- **Layer 1 (Physical):** Converts bits into WiFi or mobile signals.

---

###  OSI Step-by-Step

1. **Application:** WhatsApp starts the call.  
2. **Presentation:** Compress and encrypt voice data.  
3. **Session:** Manage and maintain the call.  
4. **Transport:** Send data using UDP packets.  
5. **Network:** Route packets with IP addresses.  
6. **Data Link:** Use MAC for local delivery.  
7. **Physical:** Send bits through WiFi or cables.

---

##  TCP/IP Model (4 Layers)

1. **Application:** WhatsApp manages call, compression, and encryption.  
2. **Transport:** Uses UDP or RTP for quick voice transfer.  
3. **Internet:** Routes packets using IP addresses.  
4. **Link:** Frames and sends data physically via WiFi or mobile network.

---

###  Summary  
The **OSI Model (7 layers)** explains networking in detail for learning,  
while the **TCP/IP Model (4 layers)** is a simplified, practical version used in real-world internet communication.

---

##  OSI vs TCP/IP Comparison

| Aspect | OSI Model | TCP/IP Model |
|--------|------------|--------------|
| Created By | ISO | US Defense Department |
| Year | 1984 | 1970s |
| Layers | 7 | 4 |
| Layer Names | Application, Presentation, Session, Transport, Network, Data Link, Physical | Application, Transport, Internet, Link |
| Type | Theoretical and educational | Practical and real-world |
| Protocols | Independent | Based on TCP/IP suite |
| Purpose | Teaching and designing networks | Real-world networking |
| Structure | Strict layer separation | Combined layers |
| Transport Protocols | TCP, UDP | TCP, UDP |
| Network Protocols | IP, ICMP, IGMP | IP, ICMP, ARP |
| Data Link | Separate layer | Included in Link layer |
| Session & Presentation | Separate layers | Part of Application layer |
| Flexibility | Detailed but complex | Simple and fast |
| Best Use | Learning and teaching | Real implementation |

---
# References

**Day 1** - [OSI Model](https://claude.ai/public/artifacts/e43d6790-fe29-45e8-887d-6f24978d1bc2?fullscreen=true)  
**Day 2** - [TCP/IP Model](https://claude.ai/public/artifacts/a1c59732-03c8-4268-bf63-c8a6b20e8c3c?fullscreen=true)  
