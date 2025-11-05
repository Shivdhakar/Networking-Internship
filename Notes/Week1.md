#  Networking Internship Notes
---

##  Day 1 — Networking Basics 

###  What is Networking?
Networking means connecting two or more devices (like computers, mobiles, laptops) so they can **share data, files, internet, and resources** with each other.

**Example:**  
When we use Wi-Fi at home — our phone, TV, laptop all connect and share internet.  
That is networking in real life.

In simple words:  
> Networking = Devices talking and sharing information

---

###  Why Networking is Important?
- Share files and data easily
- Use the same printer or internet connection for many devices
- Communicate through emails, chats, servers, cloud
- Connect offices across cities or countries

---

###  Networking Components

#### **1. Cables**
Wires that carry data signals between devices.  
Example: LAN cable (RJ-45).

#### **2. Switch**
A device that connects computers inside the same network (LAN).  
It sends data only to the correct device — like smart traffic signal.

#### **3. Router**
A router connects multiple networks and helps them communicate.  
It sends data outside the network (like your Wi-Fi router connecting to ISP).

> Switch = connects inside office/home  
> Router = connects your network to outside world (internet)

---

###  Network Topologies
Different ways to connect computers:

| Topology | Explanation | Example |
|---|---|---|
| Star | All devices connect to one central device | Home network with Wi-Fi router |
| Bus | All devices use one main cable | Old networks |
| Ring | Devices connected in circle | Some old MAN networks |
| Mesh | Each device connected to every device | Military networks / Data centers |

---

###  Types of Networks

| Type | Full Form | Use | Range |
|---|---|---|---|
| PAN | Personal Area Network | Bluetooth, Hotspot | Few meters |
| LAN | Local Area Network | Office / Home | Room to Building |
| MAN | Metropolitan Area Network | Connects buildings in city | City |
| WAN | Wide Area Network | Connects countries | Worldwide (Internet) |

---

###  Networking Issues
- Viruses & cyber attacks
- Slow speed due to high traffic
- Weak Wi-Fi signal
- Hardware failure (router, switch down)

---

##  Day 2 — LAN vs WAN & Network Planning

###  LAN vs MAN vs WAN

| Network | Range | Example |
|---|---|---|
| LAN | Small area (building) | Office Wi-Fi |
| MAN | Larger area (city) | Smart city internet |
| WAN | World-wide | Internet |

**Main Points:**
- LAN is fast & low cost
- WAN is large, slow compared to LAN, and costly
- MAN connects between LANs inside a city

---

###  Real Office Scenario (Example Plan)
Company Name: **EduTech Solutions**

| Area | Requirement |
|---|---|
| HQ (100 employees) | Fast LAN + Wi-Fi |
| Dev Center (5 km away) | Fiber link to HQ |
| Sales Teams | WAN connection |
| Work from Home | VPN access |

---

###  My Network Design Idea
- HQ uses **star topology**
- Dev centre connected through **fiber / leased line**
- Remote employees use **VPN**
- Office uses **firewall** for security

  ---
  ## [Click here to view image of types of neworks ](../Asset/types.png)

---

##  Day 3 — MAC & IP Addresses

###  What is MAC Address?
- Full form: **Media Access Control**
- It is a **unique physical address** written in hardware of device
- Assigned by manufacturer
- Example: `E8-AF-3C-45-9B-10`
- Helps devices identify each other inside **local network (LAN)**

> Think of MAC like your **permanent fingerprint**

---

###  What is IP Address?
- IP = **Internet Protocol**
- A logical address given to devices to communicate on the internet or network
- Can change (assigned by router or ISP)
- Example: `192.168.1.8`

> Think of IP like your **home address** where online data is delivered

---

###  How They Work Together (ARP)
1. You type google.com
2. Computer sends request using **IP**
3. Network finds device MAC using **ARP (Address Resolution Protocol)**
4. Data reaches device

> IP finds the location  
> MAC delivers to the exact device

---

###  Types of IP Addresses
| Type | Example | Use |
|---|---|---|
| Public IP | 203.xx.xx.xx | Used on internet (ISP gives) |
| Private IP | 192.168.x.x | Used inside LAN (router gives) |

**NAT (Network Address Translation)**  
Converts private IP to public IP for internet security & saving addresses.

---

###  Day 3 Key Line
> IP = House address  
> MAC = Room number

---

---
# References

**Day 1** - [Networking Basics](https://claude.ai/public/artifacts/e92959cb-3269-4546-b97d-e5dcd0aee458)  
**Day 2** - [Types of Networking](https://claude.ai/public/artifacts/f4b54e55-0e65-4185-8eb1-4ecbebbdf880)  


