# 📘 Day 4 - Week 2: OSI Model (Open Systems Interconnection)

The **OSI Model** is a conceptual framework used to standardize how different networking systems communicate. It divides the network communication process into **7 layers**, where each layer performs a specific role in handling and transmitting data across a network.

---

## 🧱 The 7 Layers of the OSI Model

---

### 1️⃣ Physical Layer  
- Deals with **hardware components** and the **physical transmission** of raw data (bits: 0s and 1s).  
- Includes cables, connectors, and transmission mediums.  
- **Examples:** Ethernet cables, Hubs.

---

### 2️⃣ Data Link Layer  
- Ensures **error-free transfer** of data frames between two directly connected devices.  
- Handles **MAC addressing** and frame synchronization.  
- **Examples:** Network Switches, Bridges.

---

### 3️⃣ Network Layer  
- Responsible for **logical addressing** and **routing** of packets across networks.  
- Decides the **best path** for data to reach its destination.  
- **Examples:** Routers, IPv4, IPv6.

---

### 4️⃣ Transport Layer  
- Provides **reliable or unreliable delivery** of data using protocols like **TCP** or **UDP**.  
- Handles **segmentation**, **flow control**, and **error detection/recovery**.  
- **Examples:** TCP, UDP.

---

### 5️⃣ Session Layer  
- Establishes, manages, and terminates **sessions** between two applications.  
- Supports **dialog control**, keeping data streams organized.  
- **Examples:** APIs, Remote Procedure Calls (RPC).

---

### 6️⃣ Presentation Layer  
- Translates data between the **application** and the **network format**.  
- Performs **encryption**, **decryption**, and **compression**.  
- **Examples:** SSL/TLS, JPEG, MP3.

---

### 7️⃣ Application Layer  
- Closest to the **end user**.  
- Provides **network services** like web browsing, email, and file transfer.  
- **Examples:** HTTP, FTP, SMTP, DNS.

---

## ✅ Summary Table

| Layer | Name             | Function                            | Examples               |
|-------|------------------|-------------------------------------|------------------------|
| 7     | Application       | User services                       | HTTP, FTP, SMTP, DNS   |
| 6     | Presentation      | Translation, encryption, compression| SSL/TLS, JPEG, MP3     |
| 5     | Session           | Session management                  | APIs, RPC              |
| 4     | Transport         | Reliable data delivery              | TCP, UDP               |
| 3     | Network           | Logical addressing, routing         | IP, Routers            |
| 2     | Data Link         | Frame transfer, MAC addressing      | Switches, Bridges      |
| 1     | Physical          | Hardware, bit transmission          | Ethernet, Hubs         |

---

📌 **Tip:** Think of the OSI layers like layers in a burger 🍔 — each one adds something important, and together they make networking work!

