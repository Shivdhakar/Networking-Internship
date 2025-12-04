# Router Redundancy, Firewall, and VPN  

In a corporate network, the main goals are:

- The network should not go down if one device fails.
- Data should be safe and private when it travels over the internet.
- Only authorized users should be able to access company resources.

To achieve this, companies use:

- Router redundancy  
- Firewalls  
- VPN (Virtual Private Network)  
- SSL / TLS (for secure communication)

<br/>

##  Router Redundancy

###  Why do we need router redundancy?

In a normal network, all PCs in a LAN use a **default gateway** (a router) to go outside the network.

- If that **single router** goes down:
  - Users cannot access the internet or other networks.
  - This is called a **single point of failure**.

To prevent downtime, companies use **more than one router** to provide the same gateway service.  
This concept is known as **router redundancy**.

---

###  Basic idea of router redundancy

- Two or more routers are connected to the same LAN.
- They **share one virtual IP address** which acts as the default gateway for PCs.
- From the user's point of view, there is only **one gateway IP**.

Internally, routers decide:

- Which router is **Active / Master**
- Which router is **Standby / Backup**

If the active router fails:

- The backup router **automatically takes over** the virtual IP.
- Users usually do not notice any interruption.

This is done using **First Hop Redundancy Protocols (FHRP)** such as:

- HSRP (Hot Standby Router Protocol)
- VRRP (Virtual Router Redundancy Protocol)
- GLBP (Gateway Load Balancing Protocol)

---

###  HSRP (Hot Standby Router Protocol)

- **Vendor**: Cisco proprietary
- **Working**:
  - Routers form an HSRP group.
  - They use a **virtual IP** and a **virtual MAC** address.
  - One router becomes **Active** (forwards traffic).
  - Another becomes **Standby** (ready to take over).
  - Routers send **Hello messages** to check health.

If the Active router fails:

- The Standby router becomes the new Active router automatically.

**Use Case**: Simple active–standby gateway for LANs using Cisco devices.

---
<br/>

###  VRRP (Virtual Router Redundancy Protocol)

- **Vendor**: Open standard (supports multiple vendors)
- Similar to HSRP.
- One router is **Master**, others are **Backup**.
- All share a **virtual IP**.
- If Master fails, a Backup becomes the new Master.

**Use Case**: Multi-vendor networks requiring redundancy.

---

### GLBP (Gateway Load Balancing Protocol)

- **Vendor**: Cisco proprietary
- Main difference:
  - **HSRP/VRRP**: focus on redundancy (one active at a time)
  - **GLBP**: provides both **redundancy + load balancing**

GLBP:

- Uses one virtual IP
- Uses **multiple virtual MAC addresses**
- Hosts are assigned different virtual MACs
- Traffic is **balanced across multiple routers**

If one router fails, others continue handling traffic.

**Use Case**: When both backup and load distribution are needed.

---

### Summary of HSRP vs VRRP vs GLBP

- **HSRP**  
  Cisco-only, Active–Standby, simple redundancy.

- **VRRP**  
  Open standard, Master–Backup, multi-vendor support.

- **GLBP**  
  Cisco-only, redundancy + load balancing.

---

##  Firewalls in Corporate Networks

###  What is a firewall?

A **firewall** is a security device (hardware or software) placed between:

- The **internal network (LAN)**, and  
- The **outside world (internet or other networks)**

It monitors and controls traffic based on rules.

> A firewall works like a **security guard** at the main gate of a company.

It checks:

- Who is coming in?
- Who is going out?
- Are they allowed?

---

###  Why do companies use firewalls?

- To block **unauthorized access**
- To allow only required services (HTTP, HTTPS, SSH, etc.)
- To protect against attacks (malware, hackers, port scans)
- To create different security zones:
  - Internal LAN
  - DMZ (public servers)
  - Internet

---

###  Types of Firewalls (Simple View)

#### **Packet-Filtering Firewall**
- Checks source IP, destination IP, port, and protocol.
- Uses simple ACL rules.
- Works at Network & Transport layers.

#### **Stateful Firewall**
- Remembers connection states.
- Understands new, established, and related connections.
- More secure than packet-filtering.

#### **Application Layer / Next-Gen Firewall (NGFW)**
- Understands applications like Facebook, WhatsApp, YouTube.
- Can filter by user identity.
- Offers IPS/IDS, deep packet inspection, URL filtering.

#### **Host-Based Firewall**
- Runs on individual devices (e.g., Windows Defender Firewall).

---

###  Simple Firewall Rule Example

A small company firewall may have rules like:

- Allow outgoing HTTP/HTTPS from LAN to Internet.
- Allow incoming HTTPS only to the web server in DMZ.
- Block Telnet (port 23) everywhere.
- Deny all other traffic by default.

This ensures:

- Employees can browse safely.
- Customers can access the company website.
- Dangerous services are blocked.

---

## VPN (Virtual Private Network) 

###  What is a VPN?

A **VPN** creates a **secure, encrypted tunnel** over the public Internet.

Even though traffic travels across the Internet, it behaves as if devices were inside the **same private network**.

Key points:

- Ensures privacy and security  
- Protects data from hackers/sniffers  
- Used for remote work and branch connectivity

---

###  Why do companies use VPNs?

#### **Secure Remote Access**
Employees can access internal servers, apps, and shared drives from anywhere.

#### **Connecting Branch Offices**
Site-to-Site VPN connects different office locations through the Internet.

#### **Secure Communication with Partners**
Limited access to external partners using controlled VPN access.

#### **Cost Savings**
Uses Internet instead of expensive private leased lines.

---

###  Types of VPN

#### **Site-to-Site VPN**
- Connects two or more offices.
- Uses VPN routers/firewalls.
- Often uses **IPsec**.
- Transparent for users.

Example:  
Head Office (Delhi) ⇄ IPsec VPN ⇄ Branch Office (Jaipur)

---

#### ** Remote-Access VPN**
- Used by individual employees.
- User installs VPN client software.
- Connects using username/password/OTP.
- Gets a **virtual IP** from company.

---

#### ** SSL VPN**
- Works using **HTTPS (SSL/TLS)**.
- Can be accessed through a browser or light client.
- Uses the same encryption technology as secure websites.

Example:  
Open `https://vpn.company.com` → Login → Access internal apps.

---

#### ** MPLS / Provider VPN**
- Provided by ISPs.
- Creates private networks over the provider's backbone.
- Used by large companies for stable branch connectivity.

---

##  SSL / TLS (and Example)

###  What is SSL / TLS?

SSL (Secure Sockets Layer) and TLS (Transport Layer Security) provide:

- Encryption  
- Data integrity  
- Authentication  

Whenever you see `https://`, it means the website is using **SSL/TLS**.

---

###  Why SSL/TLS Is Important?

Without encryption:

- Passwords, OTPs, bank data would be readable as plain text.
- Hackers can sniff this data.

With SSL/TLS:

- Data is encrypted.
- Even if packets are captured, they cannot be easily read.

---

###  How HTTPS (SSL/TLS) Works – Simple Steps

1. **Client Hello**  
   Browser requests a secure connection.

2. **Server Certificate**  
   Server sends a certificate issued by a CA (DigiCert, Let's Encrypt, etc.).

3. **Certificate Validation**  
   Browser checks:
   - Issuing authority
   - Expiry
   - Domain name match

4. **Key Exchange**  
   Browser creates a session key, encrypts it with the server’s public key, and sends it.

5. **Secure Session**  
   Both sides now use the session key for encryption/decryption.

Result:  
Your communication is secure and authenticated.

---

###  SSL Example Related to VPN

**Scenario: Employee using SSL VPN from home**

1. User opens:  
   `https://vpn.orphinchemistry.com`

2. The VPN gateway:
   - Sends its SSL/TLS certificate.
   - Browser validates it.

3. After validation:
   - An **HTTPS secure tunnel** is created.
   - Login details (username, password, OTP) are encrypted.

4. After login:
   - User can access internal applications.
   - All further traffic is protected through the SSL tunnel.

This is how **SSL VPN** keeps corporate data safe.

