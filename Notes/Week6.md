## DHCP, NTP & TCP Handshake (Auto IP + Time + Hello!)  
**What I Learned Today:**

**DHCP = IP Giver**  
No more typing IPs manually Router gives automatically   

**How It Works (DORA):**  
1. **Discover:** "Hey router, need IP"  
2. **Offer:** "Here's 192.168.1.10 for you"  
3. **Request:** "Cool, I'll take it!"  
4. **Acknowledge:** "Done! + mask + gateway + DNS"  

**What I Get:**  
- IP: `192.168.1.10`  
- Mask: `255.255.255.0`  
- Gateway: `192.168.1.1` (router)  
- DNS: `8.8.8.8` (Google)  
- Time limit: 24 hours  

**Ports:** Server `67` | My phone `68`  

---

# NTP (Network Time Protocol)

##  What is NTP?
NTP stands for **Network Time Protocol**.  
It is used to **synchronize the time** of all devices (like routers, switches, servers, and computers) in a network with a **central time server**.

##  How It Works
- All devices connect to an **NTP server**.
- The server provides the **correct time**.
- Devices adjust their clocks to match the server’s time.
- This keeps the **same time** across the network — important for logging, security, and communication.

##  Example
If your router and PC have different times, NTP helps both match the **exact same time** as the time server.

---

#  Three-Way Handshake (TCP Connection)

##  What is Three-Way Handshake?
It’s the process used by **TCP (Transmission Control Protocol)** to **establish a reliable connection** between two devices before sending data.

## Steps

1. **SYN (Synchronize)**  
   The client sends a request to the server to start a connection.

2. **SYN-ACK (Synchronize + Acknowledge)**  
   The server replies that it’s ready and acknowledges the client’s request.

3. **ACK (Acknowledge)**  
   The client confirms the server’s response, and the connection is established.

## Example
When you open a website:
- Your computer → sends SYN  
- Server → replies with SYN-ACK  
- Your computer → sends ACK  

Now the connection is **ready to transfer data** safely.

---

**In short:**
- **NTP** keeps network time accurate.  
- **Three-way handshake** creates a safe and reliable connection between two devices.

---

**Quick Cheat Sheet:**  
| What | Job | Port | Steps |  
|------|-----|------|-------|  
| **DHCP** | Gives IP | 67/68 | 4 (DORA) |  
| **NTP** | Sets time | 123 | 2 (ask+get) |  
| **TCP** | Starts chat | - | 3 (hello!) |  

**Real Test:**  
- Phone connected WiFi = DHCP worked! `192.168.0.105`  
- Time same on laptop+phone = NTP good!  
- Opened YouTube = TCP handshake done!   

**Memory Trick:**  
**D**HCP = **D**elivers IP  
**N**TP = **N**o time fights  
**T**CP = **T**hree hellos  

*Day 3 Done! My phone does ALL this automatically!* 
## Day 2: NAT & PAT (Router Magic!)  
**What I Figured Out Today:**

**NAT = Address Changer**  
My home WiFi has private IPs (192.168.x.x) but internet needs public IPs.  
**NAT = Router's translator!** Private → Public when I browse YouTube  

**Why Cool?**  
- Saves public IPs (only 4 billion total!)  
- Hides my home devices from hackers  
- ALL my phones/laptops share 1 public IP  

**3 Types (Simple):**  
| Type | What | Example |  
|------|------|---------|  
| **Static** | 1 phone = 1 public IP | My web server |  
| **Dynamic** | Pick from pool | Office computers |  
| **PAT** | EVERYONE shares 1 IP! | My home router |  

**PAT = NAT + Port Trick**  
Router changes **ports** so it knows who's who!  

**Real Example (My Browsing):**  
*Before:* My laptop `192.168.1.10:50000` → Google `443`  
*Router Changes:* `203.0.113.5:40001` → Google `443`  
*Google replies to:* `40001` → Router sends back to my `50000`  

**Ports = Door Numbers**  
- **80** = Normal website  
- **443** = Secure (https)  
- **My laptop picks:** Random door `50000`  
- **Router changes to:** `40001` (so no mix-up)  

**My Home Setup:**  
3 phones + 2 laptops = 5 devices  
**ALL use same public IP `203.0.113.5`**  
Router uses different ports: `40001, 40002, 40003...`  
*Google thinks it's 5 different people!*   

**Without PAT?**  
All 5 devices fight for same address = **INTERNET CRASH!**  

**Quick Test:**  
Opened 3 Chrome tabs = 3 different source ports!  
Tab1: `49152` | Tab2: `49153` | Tab3: `49154`  
*Router changed them all to unique numbers*  
 
