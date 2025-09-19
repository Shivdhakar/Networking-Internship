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











