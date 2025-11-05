#  Networking Internship Notes
---

## **Day 1 — Networking Basics**

### What I learned today

**What is Networking?**  
Networking means connecting computers and devices so they can share information.  
It's like a group chat — but instead of people, devices talk to each other.

###  Networking Components

#### **Hardware**
- **Cables** – Carry data between devices (just like wires carry electricity)
- **Switches** – Connect multiple devices and forward data inside a LAN  
  _(like a traffic police controlling vehicles)_
- **Routers** – Connect different networks and send data to the right destination  
  _(like a postmaster who decides where each letter goes)_

#### **Software**
Applications and protocols that help data travel across the network.

---

### Network Topologies (How devices are arranged)
| Topology | Meaning | Example |
|---|---|---|
| **Star** | All devices connect to a central device | Home Wi-Fi setup |
| **Bus** | All devices share one main cable | Old networks |
| **Ring** | Devices form a circle and data moves in one direction | Older LAN systems |
| **Mesh** | Every device connects to every device | Military networks (very reliable) |

---

###  Types of Networks
| Type | Full Form | Example | Coverage |
|---|---|---|---|
| **PAN** | Personal Area Network | Mobile + Bluetooth earbuds | A few meters |
| **LAN** | Local Area Network | Office / Home network | Building |
| **MAN** | Metropolitan Area Network | City-wide Wi-Fi | City |
| **WAN** | Wide Area Network | Internet | Worldwide |

---

### How Data Travels
**Send message → Breaks into packets → Travels through routers → Reaches target device**

---

###  Things that can go wrong
- Hackers & data theft
- Viruses & malware
- Slow internet due to overload
- Weak Wi-Fi signal

**Day 1 Conclusion:**  
Networking simply means devices talking and sharing data with each other.

---

## **Day 2 — LAN vs WAN & Basic Network Planning**

###  Difference between LAN, MAN, WAN

| Network | Coverage | Example |
|---|---|---|
| LAN | Building / Office | Home Wi-Fi |
| MAN | City or campus | University network |
| WAN | Country or worldwide | Internet |

---

###  Example Case Study: Small Company Network

**Company:** EduTech Solutions  
**Requirement:** Connect all offices & employees

| Location | Need |
|---|---|
| HQ (100 staff) | Fast LAN, switches, router |
| Dev Center (50 staff, 5km away) | Fiber link to HQ |
| Sales Offices | WAN / Internet connectivity |
| Remote employees | VPN access |

---

###  My Network Design Plan
- HQ: **Star topology** + high-speed switches  
- Dev center: **Leased line / Fiber**
- Sales offices: **VPN**
- Remote employees: **Secure VPN login**

###  Challenges I noticed
- Video meetings lag sometimes  
- Home Wi-Fi may be slow for remote staff  
- Security for laptops working from outside office

 ## [Click here to view image of types of neworks ](../Asset/types.png)

---

## **Day 3 — MAC & IP Addresses**

###  MAC Address
- Unique hardware address assigned to every device
- Looks like: **AA:BB:CC:DD:EE:FF**
- Used inside local network
- Fixed and cannot be changed manually

###  IP Address
- Logical address given to a device on the network
- Example: **192.168.1.10**
- Can change (assigned by router/DHCP)
- Used to communicate across networks/internet

---

###  How MAC & IP Work Together
1. Device sends data to an **IP address**
2. Router asks — "Who has this IP?" (ARP)
3. It finds the **MAC address**
4. Data goes to correct device

**Simple example:**  
IP = Home address  
MAC = Door number (specific to your room)

---

###  My Small Test
- My phone MAC: `E8:XX:XX:XX:XX:XX`
- My phone IP: `192.168.0.105`

###  Why Private IPs are needed
- Protect devices from hackers  
- Avoid IP shortage  
- NAT hides internal IPs and keeps devices secure

---

###  Day 3 Summary
**IP = Where the device is on the network**  
**MAC = Who exactly the device is**



---
# References

**Day 1** - [Networking Basics](https://claude.ai/public/artifacts/e92959cb-3269-4546-b97d-e5dcd0aee458)  
**Day 2** - [Types of Networking](https://claude.ai/public/artifacts/f4b54e55-0e65-4185-8eb1-4ecbebbdf880)  


