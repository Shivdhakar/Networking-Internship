#  Networking Internship Notes

---

##  **Day 1: Networking Basics**

###  What I Picked Up Today:
**Networking?**  
It's like devices chatting with each other — just like a group chat but for computers and gadgets.

---

###  Key Parts:
**Hardware:**
- **Cables:** Carry data (like wires in electricity).
- **Switches:** Direct the data (like traffic police).
- **Routers:** Sort and send data (like post offices).

**Software:**
- Apps and programs that help data move from one place to another.

---

###  Network Topologies (Layouts):
- **Star:** All connect to one hub (like home Wi-Fi router).  
- **Bus:** All devices in one line (old style).  
- **Ring:** Data travels in a circle.  
- **Mesh:** Everyone connects to everyone (strong but costly).

---

###  Network Sizes:
| Type | Full Form | Example | Range |
|------|------------|----------|-------|
| PAN | Personal Area Network | Phone ↔ Earbuds | Few feet |
| LAN | Local Area Network | Office or Home | Building level |
| MAN | Metropolitan Area Network | City Wi-Fi | City-wide |
| WAN | Wide Area Network | Internet | Global |

---

###  Data Flow:
**Click Send → Data splits into packets → Travels via router → Reaches destination device**

---

###  Issues to Watch:
- Hackers stealing info  
- Viruses  
- Lag from overload  
- Weak Wi-Fi signals  

 **Day 1 Wrapped!**  
Networking = Gadgets chatting with each other. Simple!

---

##  **Day 2: LAN vs WAN + Planning**

###  Quick Compare:
| Type | Range | Example |
|------|--------|----------|
| LAN | Small (Room to Building) | Office |
| MAN | Medium (Campus or City) | University |
| WAN | Large (Country to Country) | Internet |

---

###  Company Example: *EduTech Solutions*
- **HQ:** 100 staff (need fast LAN)  
- **Dev Center:** 50 devs, 5km away (fiber link)  
- **Sales Offices:** State-wide (WAN connection)  
- **Remote Workers:** 25 people via VPN  

---

###  My Network Design:
- **HQ:** Star topology with high-speed switches  
- **Dev Site:** Leased line connection  
- **Sales Offices:** VPN links  
- **Remotes:** Company VPN access  

---

###  Hurdles:
- Smooth video meetings  
- Laptop security risks  
- Slow home internet speeds  

 *Diagram sketch planned for tomorrow!*

---

## [Click here to view image of types of neworks ](../Asset/types.png)

---


##  **Day 3: MAC & IP Addresses (Clicked Finally!)**

###  MAC Address:
- Built-in hardware ID → Example: `AA:BB:CC:DD:EE:FF`  
- Used inside local network only  
- Permanent and unique  
- Cannot be changed manually  

---

###  IP Address:
- Temporary digital address → Example: `192.168.1.10`  
- Works globally  
- Assigned automatically by **DHCP** via router  

---

###  How They Work Together:
1. You send data to an **IP** address.  
2. Router asks via **ARP:** “Who owns this IP?”  
3. Gets the **MAC** address.  
4. Sends the data — IP for routing, MAC for final delivery.

---

###  IP Types:

| Type | Example | Use |
|------|----------|-----|
| Public | 8.8.8.8 | Used on the open internet |
| Private | 192.168.1.1 | Used in home/office networks |

---

###  My Setup:
- **ISP Router:** Public IP (like `203.xxx.xxx.xxx`)  
- **My Phone:** Private IP (`192.168.1.5`)  
- **NAT:** Hides private IP, keeps data secure.  

---

###  Without Private IPs:
- Too few addresses for billions of devices  
- No hiding layer  
- Easy hacking  
- Internet chaos! 

---

###  My Test:
- **Phone MAC:** `E8:XX:XX:XX:XX:XX`  
- **Phone IP:** `192.168.0.105`  

 **Day 3 Summary:**  
**IP = Street address, MAC = Door number. Nailed it!**

---
# References

**Day 1** - [Networking Basics](https://claude.ai/public/artifacts/e92959cb-3269-4546-b97d-e5dcd0aee458)  
**Day 2** - [Types of Networking](https://claude.ai/public/artifacts/f4b54e55-0e65-4185-8eb1-4ecbebbdf880)  


