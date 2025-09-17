# Day 1: Networking Basics
# Networking Internship Notes

Welcome to my Networking Internship notes repository. This repo contains a detailed summary of my learning journey through the internship, covering fundamental networking concepts, network planning, and addressing schemes.

---

## Day 1: Networking Basics

**Topics Covered:**

- **What is Networking?**  
  Understanding the fundamental definition and purpose.

- **Components of Networking:**  
  Key hardware and software involved in networks.

- **Network Topologies:**  
  - Star  
  - Bus  
  - Ring  
  - Mesh  

- **Types of Networks:**  
  - PAN (Personal Area Network)  
  - LAN (Local Area Network)  
  - MAN (Metropolitan Area Network)  
  - WAN (Wide Area Network)  

- **Basic Network Flow:**  
  How data travels across networks.

- **Common Network Challenges:**  
  - Unauthorized Access  
  - Data Breach  
  - Viruses  

- **Network Performance Issues:**  
  - Network Congestion  
  - Connection Reliability  
  - Bandwidth Limitations  

---

## Day 2: Deep Dive into LAN, MAN, and WAN + Network Planning Exercise

### Learning Focus:
Understanding differences between LAN, MAN, WAN and designing network architecture.

---

### Network Planning Scenario:

**Client:** EduTech Solutions — an educational software company

- **Main Office:** 100 employees, downtown  
- **Development Center:** 50 employees, 5 km away  
- **Regional Sales Offices:** 3 locations across the state  
- **Remote Workers:** 25 employees working from home  

---

### Task: Design Network Architecture

| Location               | Network Type | Notes/Reasoning                                 |
|------------------------|--------------|------------------------------------------------|
| Main Office            | LAN          | Local area network to connect all employees onsite |
| Development Center     | MAN          | Connects nearby office within metropolitan area |
| Regional Sales Offices | WAN          | Connect offices across the state (wide area)  |
| Remote Workers        | WAN (VPN)     | Remote access through VPN over the internet    |

---

## Day 3: Understanding MAC and IP Addresses

### Network Addresses Overview

- **MAC Address (Physical Address):**  
  - Hardcoded into the Network Interface Card (NIC)  
  - Unique worldwide identifier  
  - 48-bit (6 pairs of hexadecimal digits)  
  - Operates at Layer 2 (Data Link Layer)  
  - Non-routable beyond local network segment  

- **IP Address (Logical Address):**  
  - Assigned by network configuration (manual or DHCP)  
  - Composed of Network and Host portions  
  - IPv4 is 32-bit (4 decimal groups from 0-255)  
  - Operates at Layer 3 (Network Layer)  
  - Routable across different networks  

---

### How MAC and IP Work Together

- MAC identifies devices locally within a LAN.  
- IP allows devices to communicate across different networks.

---

### Packet Transmission & ARP

- Packets are data units sent from source to destination.  
- Address Resolution Protocol (ARP) translates IP addresses to MAC addresses within local networks.

---

### IP Addressing Summary

1. **What is an IP Address?**  
   A unique digital address for a device enabling communication.

2. **Types of IP Addresses:**  

| Type       | Description                         |
|------------|-----------------------------------|
| Public IP  | Assigned by ISP, used on the Internet |
| Private IP | Used within local/private networks  |

3. **IP Classes and Private Ranges:**  
   Networks are divided to organize, allocate, and route IPs efficiently.

4. **Why Classes?**  
   - Match network sizes  
   - Simplify IP management and routing  
   - Reserve private IPs for internal use  

5. **Home Wi-Fi Setup:**  
   - ISP assigns a public IP to your router  
   - Router assigns private IPs (e.g., 192.168.x.x) to your devices  
   - Private network connects to the public internet via NAT  

6. **Role of Towers and Routers:**  
   - Public IPs assigned to these devices by ISP  
   - Use DHCP to assign private IPs to connected devices  
   - NAT translates private IPs to public for internet access  

7. **If IPs Were Not Divided:**  
   - IP conflicts and routing issues would arise  
   - Internet management and security would be compromised  

---

### Final Summary

- Public IPs are assigned by ISPs to routers and towers.  
- Routers assign private IPs to local devices.  
- IP division into classes ensures organized, scalable, and secure networking.

---

Feel free to explore and reach out if you want to discuss anything related to networking!

---

*Last updated: 2025-09-17*

---

