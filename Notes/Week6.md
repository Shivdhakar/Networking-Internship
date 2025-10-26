# Networking Notes: DHCP, NTP, Handshake, NAT/PAT


##  DHCP: The IP Handout Hero

**DHCP (Dynamic Host Configuration Protocol)** is like your network’s auto-IP distributor.

Imagine a single laptop on home Wi-Fi — you can manually set the IP.  
Now scale that to 50+ devices in an office — chaos! DHCP swoops in to auto-assign IPs from a pool, preventing duplicates and admin headaches.

**Why It Matters:**  
Big networks depend on it — plug in and connect instantly.  
In our lab, without DHCP = devices lost; with DHCP = instant online.

---

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

---

###  Core Components

- **Server:** The boss. Holds IP pool, leases IPs, gateway, DNS.  
- **Client:** Any device — asks for IP.  
- **Pool:** IP range like `10.0.0.10-50`.  
- **Lease:** Time-limited usage. Expires and returns to pool.

**Example:** Pool `192.168.1.100–200`, lease = 1 day → 20 clients joined automatically.

---

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

---

###  Assignment Flavors

- **Dynamic:** Temporary pool IP (most common).  
- **Automatic:** One-time permanent IP.  
- **Static:** Reserved per MAC (used for printers/servers).

Dynamic is the go-to — perfect for mobile or temporary connections.

---

###  Lease Renewal: T1, T2 & Expiry

1. **T1 (50%)** → Client quietly asks to renew lease.  
2. **T2 (87.5%)** → No reply? Broadcasts to all servers.  
3. **Expiration** → Lease gone, restart DORA.

We tested this by setting a 5-minute lease — renewal worked flawlessly.

---

 *Lab Capture:* Wireshark DORA trace — showed DISCOVER → OFFER → REQUEST → ACK clearly.  
 *Takeaway:* DHCP = Plug & Play networking. Without it = network chaos.

---

##  NTP: The Clock Sync Squad

**NTP (Network Time Protocol)** keeps all devices’ clocks accurate to UTC.

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

---

##  TCP 3-Way Handshake: Building Trust

TCP’s **3-way handshake** ensures reliable communication before any data exchange.

1. **SYN:** Client → “Let’s connect!” (Sync flag).  
2. **SYN-ACK:** Server → “I’m ready!” (Sync + Ack).  
3. **ACK:** Client → “Got it!” (Ack flag). Connection established.

After this, data flows smoothly — ordered and error-checked.  
In our lab, missing a SYN meant **no connection** — TCP doesn’t compromise on trust.

 **Tools Used:** `tcpdump`, Wireshark → saw SYN → SYN-ACK → ACK in real-time.

---

##  NAT & PAT: IP Masquerade Masters

**NAT (Network Address Translation)** translates private IPs into public IPs for Internet access.  
Essential for IPv4’s limited address space.

###  How It Works

Private network → Router (NAT-enabled) → Public Internet.  
Replies come back to router → router maps back to private host.

**Purpose:**
- Share one public IP among multiple devices.  
- Add a security layer (hide internal IPs).  
- Simplify public-facing infrastructure.

---

###  Types of NAT

| Type | Description | Example |
|------|--------------|----------|
| **Static NAT** | 1:1 mapping (private ↔ public) | 192.168.1.10 → 203.0.113.10 |
| **Dynamic NAT** | Private IP temporarily mapped from a public pool | Temporary outbound IP |
| **PAT (Port Address Translation)** | Many private IPs share one public IP using ports | 192.168.1.10:80 → 203.0.113.1:5000 |

**PAT** is the real MVP — allows 100s of users behind one public IP by mapping unique port numbers.

---

###  Real-World Uses

- **Corporate Web Access:** 100 employees share 5 public IPs via PAT.  
- **Hosting Servers:** Static NAT exposes selected services.  
- **Security:** Masks internal IPs from hackers.  
- **Cloud Gateways:** Segment and control access.  
- **Development Labs:** Use fake private IPs to simulate production.

**Lab:** Configured 5 VMs under one public IP using PAT — checked via router logs. No conflicts!

---

 *Diagram Ref:* NAT flow — Private ↔ Public translation.  
 *Day 14 Summary:* NAT/PAT = Network chameleons — hide, share, secure.

---

##  Wrap-Up

**DHCP:** Auto IP allocation.  
**NTP:** Time sync backbone.  
**TCP Handshake:** Reliable connection setup.  
**NAT/PAT:** IP sharing and protection.

All four form the **foundation of modern networking** — and every IT or network admin must master them.

*Next up:* VLANs and Subnets — where segmentation gets spicy. 🔥
