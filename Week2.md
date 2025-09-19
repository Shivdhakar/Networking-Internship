#  Day 4 - Week 2: OSI Model (Open Systems Interconnection)

The **OSI Model** is a conceptual framework used to standardize how different networking systems communicate. It divides the network communication process into **7 layers**, where each layer performs a specific role in handling and transmitting data across a network.


## The 7 Layers of the OSI Model


### Physical Layer  
- Deals with **hardware components** and the **physical transmission** of raw data (bits: 0s and 1s).  
- Includes cables, connectors, and transmission mediums.  
- **Examples:** Ethernet cables, Hubs.


###  Data Link Layer  
- Ensures **error-free transfer** of data frames between two directly connected devices.  
- Handles **MAC addressing** and frame synchronization.  
- **Examples:** Network Switches, Bridges.


###  Network Layer  
- Responsible for **logical addressing** and **routing** of packets across networks.  
- Decides the **best path** for data to reach its destination.  
- **Examples:** Routers, IPv4, IPv6.


###  Transport Layer  
- Provides **reliable or unreliable delivery** of data using protocols like **TCP** or **UDP**.  
- Handles **segmentation**, **flow control**, and **error detection/recovery**.  
- **Examples:** TCP, UDP.


###  Session Layer  
- Establishes, manages, and terminates **sessions** between two applications.  
- Supports **dialog control**, keeping data streams organized.  
- **Examples:** APIs, Remote Procedure Calls (RPC).


###  Presentation Layer  
- Translates data between the **application** and the **network format**.  
- Performs **encryption**, **decryption**, and **compression**.  
- **Examples:** SSL/TLS, JPEG, MP3.


###  Application Layer  
- Closest to the **end user**.  
- Provides **network services** like web browsing, email, and file transfer.  
- **Examples:** HTTP, FTP, SMTP, DNS.


##  Summary Table

| Layer | Name             | Function                            | Examples               |
|-------|------------------|-------------------------------------|------------------------|
| 7     | Application       | User services                       | HTTP, FTP, SMTP, DNS   |
| 6     | Presentation      | Translation, encryption, compression| SSL/TLS, JPEG, MP3     |
| 5     | Session           | Session management                  | APIs, RPC              |
| 4     | Transport         | Reliable data delivery              | TCP, UDP               |
| 3     | Network           | Logical addressing, routing         | IP, Routers            |
| 2     | Data Link         | Frame transfer, MAC addressing      | Switches, Bridges      |
| 1     | Physical          | Hardware, bit transmission          | Ethernet, Hubs         |




















## Example : Voice Call Using VoIP (e.g., WhatsApp Call) – OSI Model Breakdown



When you make a voice call using a VoIP app like WhatsApp, all 7 OSI layers work together to send your voice as data over the internet.

- **Layer 7: Application**  
  WhatsApp uses VoIP services to initiate and manage the call. The app handles call setup, user interface, and signaling.

- **Layer 6: Presentation**  
  Your voice is converted into digital audio, then **compressed** using codecs like **Opus** to reduce size without losing quality.

- **Layer 5: Session**  
  A session is established between your device and the receiver's device to maintain the call connection and control.

- **Layer 4: Transport**  
  Voice data is sent using **UDP** (User Datagram Protocol), which allows for faster delivery but with less reliability—ideal for real-time audio.

- **Layer 3: Network**  
  The data packets are routed across the internet to the recipient’s IP address using **IPv4** or **IPv6** protocols.

- **Layer 2: Data Link**  
  The data frames are transmitted over the local network (Wi-Fi or cellular) using MAC addressing.

- **Layer 1: Physical**  
  The digital data is sent as electrical signals over Wi-Fi, cellular radio waves, or Ethernet cables.







### 🔹 Using the OSI Model (7 Layers)

1. **Application Layer (7)**  
   - WhatsApp initiates the voice call.
   - Handles signaling, call setup, and UI interaction.

2. **Presentation Layer (6)**  
   - The voice is **compressed** using codecs like **Opus**.
   - If enabled, the call is **encrypted** (e.g., end-to-end encryption).

3. **Session Layer (5)**  
   - A **session** is established between both devices.
   - Manages the control and flow of the call.

4. **Transport Layer (4)**  
   - Uses **UDP** for fast delivery of voice packets.
   - Some real-time calls may use **RTP** (Real-time Transport Protocol) on top of UDP.

5. **Network Layer (3)**  
   - Each packet is addressed with an **IP address**.
   - Routers forward the packets across the internet to the receiver.

6. **Data Link Layer (2)**  
   - Uses **MAC addresses** to deliver frames within the local network.
   - Data is framed and checked for errors.

7. **Physical Layer (1)**  
   - Bits (0s and 1s) are transmitted over **Wi-Fi**, **4G/5G**, or **Ethernet**.
   - This is the hardware layer — signal transmission.

---

### 🔹 Using the TCP/IP Model (4 Layers)

1. **Application Layer**  
   - WhatsApp manages the voice call interface and signaling.
   - Handles codecs, compression, and encryption.

2. **Transport Layer**  
   - Voice data is sent using **UDP**, optionally with **RTP**.
   - Focuses on speed rather than reliability (real-time).

3. **Internet Layer**  
   - Assigns and routes **IP packets** from your device to the recipient.

4. **Link Layer**  
   - Handles framing, MAC addressing, and transmission over the **physical medium** (Wi-Fi, cellular, Ethernet).

---

### 🧠 Summary

- In the **OSI Model**, the process is broken into **7 detailed layers**, each with specific roles (like Session and Presentation).
- In the **TCP/IP Model**, the process is more practical, combining those into **4 layers**.
- Regardless of the model, the data flow and purpose are the same: convert your voice into data, send it, and play it back at the other end — all in real-time.


## 📊 Detailed Comparison Table: OSI Model vs TCP/IP Model

| Feature                        | OSI Model                             | TCP/IP Model                          |
|--------------------------------|----------------------------------------|----------------------------------------|
| **Developed By**              | ISO (International Standards Organization) | U.S. Department of Defense         |
| **Year Introduced**           | 1984                                   | 1970s                                 |
| **Number of Layers**          | 7 Layers                               | 4 Layers                               |
| **Layer Names**               | Application, Presentation, Session, Transport, Network, Data Link, Physical | Application, Transport, Internet, Link |
| **Usage Type**                | Conceptual/Theoretical model           | Practical/Implemented model            |
| **Protocol Dependency**       | Protocol-independent                   | Protocol-oriented                      |
| **Real-World Use**            | Mainly used for teaching/reference     | Used in real-world network communication (e.g., Internet) |
| **Approach**                  | Vertical and layered separation        | Layer merging (simplified)             |
| **Transport Layer Protocols** | TCP, UDP                               | TCP, UDP                               |
| **Network Layer Protocols**   | IP, ICMP, IGMP                         | IP, ICMP, ARP                          |
| **Data Link Layer**           | Separate layer for framing, MAC        | Merged into Link layer                 |
| **Session & Presentation**    | Separate layers                        | Included in Application layer          |
| **Flexibility**               | More detailed but less practical       | More flexible and efficient            |
| **Preferred For**             | Understanding and designing networks   | Actual implementation (Internet stack) |






