# Networking Internship Notes

## Day 1: Networking Basics
**What I Learned:**

**Networking?**  
Just computers talking to each other! 

**Main Parts:**  
- Cables, switches, routers (hardware)  
- Software that makes it work  

**Shapes (Topologies):**  
- **Star** - Everything connects to center (like my home WiFi)  
- **Bus** - All in one line  
- **Ring** - Circle  
- **Mesh** - Everyone connected to everyone  

**Network Types:**  
- **PAN** - My phone + earbuds  
- **LAN** - Office WiFi  
- **MAN** - City networks  
- **WAN** - Internet!  

**How Data Moves:**  
Send → Receive → Done  

**Problems:**  
- Hackers stealing stuff  
- Virus attacks  
- Slow internet (too many people online)  

---

## Day 2: LAN vs WAN  
**Quick Diff:**  
- **LAN** = Small (office)  
- **WAN** = Big (whole city/internet)  

**My Scenario:**  
EduTech company needs network:  
- Main office (100 ppl)  
- Dev center (50 ppl, 5km away)  
- 3 sales offices  
- 25 home workers  

*Gonna design this soon!*  

---

## Day 3: MAC & IP Addresses  
**MAC Address:**  
- Phone's real name (stuck in hardware)  
- Looks like: AA:BB:CC:DD:EE:FF  
- Only works in same room  

**IP Address:**  
- Internet name (changes)  
- Looks like: 192.168.1.1  
- Works anywhere online  

**How They Team Up:**  
IP = "Send to this house"  
MAC = "Give to this person inside"  

**ARP Magic:**  
IP → MAC translator for local network  

**IP Types:**  
- **Public** = Internet address  
- **Private** = Home WiFi (192.168.x.x)  

**My Home Setup:**  
ISP gives router public IP  
Router gives me private IP  
NAT hides my private IP online  

**Without Private IPs?**  
Everyone fighting for same address = CHAOS!  

*Finally get it! IPs = addresses, MAC = ID card* 
