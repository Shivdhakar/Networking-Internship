# Networking Notes:


##  DHCP: (Dynamic Host Configuration Protocol)

**DHCP is a network protocol that automatically assigns IP addresses and other network settings to devices when they connect to a network. Imagine if you had to manually give an IP address to every phone, laptop, or printer in your home or office—it would take forever and lead to mistakes. DHCP makes this automatic. When a device joins a network, it sends a request asking for an IP address. The DHCP server listens and responds with all the required information such as the IP address, subnet mask, default gateway, and DNS server. This process is quick and happens every time a new device connects. It works in four main steps: Discover, Offer, Request, and Acknowledge (often remembered as DORA). This ensures that every device gets a unique address and can communicate properly on the network without manual setup.

**Why It Matters:**  
Big networks depend on it — plug in and connect instantly.  
In our lab, without DHCP = devices lost; with DHCP = instant online.

###  DHCP’s Dual Table Trick

DHCP handles two main styles — static and dynamic — like a reservation list.

**Static (Manual-Style):**

| Device | IP Address |
|--------|-------------|
| Laptop | 10.0.0.1    |
| Mobile | 10.0.0.2    |
| PC     | 10.0.0.3    |

**Dynamic (Lease-Based):**

| Device | IP Address | Lease Time |
|--------|-------------|-------------|
| Laptop | 10.0.0.1    | 10 min      |
| Mobile | 10.0.0.2    | 20 min      |
| PC     | 10.0.0.3    | 5 min       |

- **Static:** Pre-assigned to MAC (servers love this).  
- **Dynamic:** Client requests IP; server assigns from pool.

We saw this live — a phone got `10.0.0.5` on boot, and boom, connected.

###  Core Components

- **Server:** The boss. Holds IP pool, leases IPs, gateway, DNS.  
- **Client:** Any device — asks for IP.  
- **Pool:** IP range like `10.0.0.10-50`.  
- **Lease:** Time-limited usage. Expires and returns to pool.

**Example:** Pool `192.168.1.100–200`, lease = 1 day → 20 clients joined automatically.

###  DORA: The 4-Step IP Dance

DHCP uses **DORA** for automatic configuration:

1. **DISCOVER:** Client broadcasts → “Who can give me an IP?”  
2. **OFFER:** DHCP server offers IP with gateway/DNS.  
3. **REQUEST:** Client requests offered IP.  
4. **ACK:** Server confirms lease → “You’re online!”

**Ports:**  
- Server → UDP 67  
- Client → UDP 68  

Captured in **Wireshark**, DORA looked like a 4-step handshake in action.

###  Assignment Flavors

- **Dynamic:** Temporary pool IP (most common).  
- **Automatic:** One-time permanent IP.  
- **Static:** Reserved per MAC (used for printers/servers).

Dynamic is the go-to — perfect for mobile or temporary connections.

###  Lease Renewal: T1, T2 & Expiry

1. **T1 (50%)** → Client quietly asks to renew lease.  
2. **T2 (87.5%)** → No reply? Broadcasts to all servers.  
3. **Expiration** → Lease gone, restart DORA.


##  NTP: (Network Time Protocol)

**NTP is a protocol that keeps all devices on a network synchronized with the same accurate time. Time synchronization might sound simple, but it’s very important in networking. Think of things like log files, scheduled backups, security certificates, or even financial transactions—they all depend on precise timing. NTP works by connecting computers and routers to a central time source called an NTP server, which gets the exact time from an atomic clock or GPS system. Devices then adjust their clocks to match that source. This way, all systems—whether in the same office or spread across the world—stay in perfect time alignment. Without NTP, data logs would become confusing and time-based processes could fail or show incorrect information.

**Why It’s Important:**  
- SSL certificates fail if clocks are wrong.  
- Logs depend on accurate timestamps.  
- File servers and backups rely on synced time.

**How It Works:**
1. Client requests time from NTP server.  
2. Server replies with precise time + delay offsets.  
3. Client adjusts its clock.

**Stratum Levels:**  
Level 1 (Atomic Clock) → Level 2 → Clients.

**Lab Result:** Our VM synced to `pool.ntp.org`, corrected a 2-second drift.  
Without NTP, authentication (SSL/TLS) breaks easily.


##  TCP 3-Way Handshake: Building Trust

TCP’s **The three-way handshake is the process used by the TCP (Transmission Control Protocol) to establish a reliable connection between two devices before data is sent. Think of it like saying hello before starting a conversation. The process happens in three steps. First, the client sends a message called SYN (synchronize) to the server to start communication. Second, the server replies with SYN-ACK (synchronize–acknowledge) to confirm it’s ready. Finally, the client sends ACK (acknowledge) back to confirm the connection. After these three steps, both sides know they’re ready to communicate and can begin transferring data securely. This handshake ensures a stable and reliable connection where both devices agree on how to send and receive information, reducing errors and connection failures.

1. **SYN:** Client → “Let’s connect!” (Sync flag).  
2. **SYN-ACK:** Server → “I’m ready!” (Sync + Ack).  
3. **ACK:** Client → “Got it!” (Ack flag). Connection established.

After this, data flows smoothly — ordered and error-checked.  
In our lab, missing a SYN meant **no connection** — TCP doesn’t compromise on trust.

 **Tools Used:** `tcpdump`, Wireshark → saw SYN → SYN-ACK → ACK in real-time.


##  NAT & PAT: (Network Address Translation / Port Address Translation)

**NAT is a technique used in routers to allow multiple devices on a private network to share a single public IP address when accessing the Internet. For example, in your home network, your phone, laptop, and TV all connect through the same Wi-Fi router, but from the Internet’s point of view, they appear as one device with one IP address. NAT works by translating the private IP addresses of these devices into the router’s public IP before sending data to the Internet, and then back again when data returns. PAT, or Port Address Translation (sometimes called NAT Overload), takes this a step further. It not only translates IP addresses but also assigns a unique port number to each connection. This allows hundreds of devices to use the same public IP address without confusion. NAT and PAT help conserve the limited number of IPv4 addresses and provide an extra layer of security by hiding internal network details from the outside world.

###  How It Works

Private network → Router (NAT-enabled) → Public Internet.  
Replies come back to router → router maps back to private host.

**Purpose:**
- Share one public IP among multiple devices.  
- Add a security layer (hide internal IPs).  
- Simplify public-facing infrastructure.

###  Types of NAT

| Type | Description | Example |
|------|--------------|----------|
| **Static NAT** | 1:1 mapping (private ↔ public) | 192.168.1.10 → 203.0.113.10 |
| **Dynamic NAT** | Private IP temporarily mapped from a public pool | Temporary outbound IP |
| **PAT (Port Address Translation)** | Many private IPs share one public IP using ports | 192.168.1.10:80 → 203.0.113.1:5000 |

**PAT** is the real MVP — allows 100s of users behind one public IP by mapping unique port numbers.

###  Real-World Uses

- **Corporate Web Access:** 100 employees share 5 public IPs via PAT.  
- **Hosting Servers:** Static NAT exposes selected services.  
- **Security:** Masks internal IPs from hackers.  
- **Cloud Gateways:** Segment and control access.  
- **Development Labs:** Use fake private IPs to simulate production.

**Lab:** Configured 5 VMs under one public IP using PAT — checked via router logs. No conflicts!

##  Mix-Up

**DHCP:** Auto IP allocation.  
**NTP:** Time sync backbone.  
**TCP Handshake:** Reliable connection setup.  
**NAT/PAT:** IP sharing and protection.

All four form the **foundation of modern networking** — and every IT or network admin must master them.
 

# References

**Day 1** - [DHCP](https://claude.ai/public/artifacts/cab20ca6-7445-4439-880e-78db376be78c) 

**Day 2** - [NAT/PAT](https://claude.ai/public/artifacts/553de791-6828-4740-becf-0fb4af7e53b7)  
