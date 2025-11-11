# Networking Internship Notes:

## Access Control Lists (ACLs): The Net's Bouncer

**ACLs are rules used in routers and switches to control which network traffic is allowed or denied. Think of them like security guards standing at the entrance of a building, deciding who can go in or out. Each rule in an ACL defines conditions based on factors like IP address, protocol type, or port number. When data packets arrive at a device, the ACL checks each packet against its list of rules and either permits or blocks it accordingly. There are two main types of ACLs: Standard ACLs, which filter traffic based only on the source IP address, and Extended ACLs, which can filter based on both source and destination IP, as well as specific ports and protocols (like HTTP or FTP). ACLs help improve network security by preventing unauthorized access, controlling data flow, and reducing unnecessary traffic. For example, you could configure an ACL to block all external users from accessing internal servers, while still allowing employees to connect freely.

###  ACLs Rule
- **Security:** Block bad IPs (spoofs, DDoS).  
- **QoS:** Prioritize VoIP over email.  
- **Compliance:** Audit trails, segment nets.  
- **Catch:** Applied inbound/outbound—order matters (top-down match).

**Lab:**  
`access-list 101 permit tcp any any eq 80` — web flew, FTP bounced. Misorder? Chaos.

### Types of ACLs
- **Standard (1–99):** Filter by source IP only.  
- **Extended (100–199):** Filter by IP, protocol, and ports.  
- **Named:** Easier to read (`ip access-list extended BLOCKBAD`).  
- **Reflexive:** Temporary, state-aware for replies.  
- **MAC:** Works on Layer 2, rarely used.

### How It Flows
1. Packet hits the interface.  
2. ACL checks from top to bottom — first match wins.  
3. Log activity if enabled (`log` keyword).  
4. Apply with: `ip access-group 101 in`  

**Wildcard Masks:**  
Inverse subnet masks — `0.0.0.255` means “any last octet.”  
Example: Blocked subnet traced denies using wildcard.

### Tips
- Place ACLs **near the source** to save CPU.  
- Use `show access-lists` to monitor hits.  
- Secure VTY (Telnet/SSH) access using ACLs.

 **Summary:** ACLs = network’s velvet rope — control without chaos.

## LAN Switching : L2 Ops Unpacked

**L2 switching refers to how data is transferred within a local network using MAC addresses. It operates at Layer 2 of the OSI model (the Data Link Layer). A Layer 2 switch doesn’t care about IP addresses—it focuses on the physical addresses (MAC addresses) of devices connected to it. When a device sends data, the switch looks at the destination MAC address and forwards the frame only to the correct port instead of sending it to everyone. This improves performance and security within the local network. L2 switches can also create VLANs (Virtual LANs) to divide a network into smaller, isolated sections—like creating separate lanes for different departments in an office. This helps reduce network congestion and keeps sensitive traffic separate. In short, L2 switching makes communication within a LAN faster, smarter, and more organized by learning where each device is connected and sending data directly to it.

### Core Gears
- **MAC Table (CAM):** Learns source MACs → ports. Ages out after ~300s.  
- **Forwarding:**  
  - Unicast → specific port.  
  - Broadcast → all ports in VLAN.  
  - Multicast → IGMP snooping helps control.  
- **Collision Domains:** Each port = one domain.  
- **Broadcast Domains:** Each VLAN = one domain.


### Operation Steps
1. **Learn:** Records source MAC and port.  
2. **Forward:** Sends frames to correct destination.  
3. **Filter:** STP blocks loops; VLAN tags segment networks.  
4. **Check Errors:** CRC ensures integrity.

### Switching Methods
- **Store-and-Forward:** Full frame check (accurate but slow).  
- **Cut-Through:** Forwards early (fast but risky).  
- **Fragment-Free:** Middle ground — checks 64 bytes.  

### Security & VLAN
- **Port Security:** Limit MACs per port, block intruders.  
- **VLAN Trunking (802.1Q):** Carries multiple VLANs on one link.  

**Lab Note:**  
Flood storm before learning — chaos. Once MAC learned — instant calm.  
L2 = local postman delivering right at the door.

## WAN Technologies: MPLS, Leased Lines, Broadband

**Wide Area Networks (WANs)** 
WAN technologies are the methods and connections used to link multiple local networks across long distances—like connecting branch offices in different cities or countries. While a LAN connects computers within one building, a WAN (Wide Area Network) connects networks over large geographic areas using communication providers like ISPs or telecom companies. Common WAN technologies include MPLS (Multiprotocol Label Switching), Leased Lines, Frame Relay, ATM, and modern solutions like SD-WAN (Software Defined WAN). These technologies use different ways to transmit data, such as fiber optics, satellite links, or wireless communication. The main goal of a WAN is to allow organizations to share data and applications securely across distant locations. For example, a company’s head office in Delhi and branch office in Mumbai can communicate as if they were in the same building, thanks to WAN technology. It ensures reliable, high-speed connectivity for remote users and supports the backbone of corporate and global communications.
### MPLS: Label Magic for Traffic

**MPLS (Multiprotocol Label Switching)** = Layer 2.5 hybrid.  
Labels packets instead of using IP lookups — fast and QoS-friendly.  
Like express lanes for data.

#### Key Points
- **Labels:** 20-bit tags; added at edge routers (LER), swapped in core (LSR).  
- **Types:**  
  - **L3VPN:** Routed (BGP-based).  
  - **L2VPN:** Bridged (Ethernet).  
- **Perks:**  
  - Traffic engineering (custom paths).  
  - QoS prioritization.  
  - Scalable any-to-any connectivity.  

**Lab:**  
Simulated MPLS VPN — seamless pings between sites. Used `show mpls forwarding` to verify labels.

 **Pros:** High speed, reliability, QoS  
 **Cons:** Complex setup, provider dependency


### Leased Lines: Your Private Highway

Dedicated, point-to-point circuits — symmetric and constant speed.  
It’s like renting your own private lane.

#### Details
- **Tech:** T1/E1 (1.5–2 Mbps) → STM/OC circuits (up to 10G).  
- **Medium:** Copper, fiber, SDH/SONET.  
- **Gear:** CSU/DSU for clock sync.  

**Pros:**  
- Reliable (99.99% uptime)  
- Secure (physically isolated)  
- Consistent bandwidth  

**Cons:**  
- Expensive  
- Limited flexibility  


### Broadband: Shared Speed Burst

**Broadband** = shared high-speed internet — ideal for homes/offices, not for mission-critical sites.

#### Common Types
- **DSL:** Uses phone line (ADSL/VDSL), up to 100 Mbps down.  
- **Cable:** Over coax (DOCSIS), up to 1 Gbps, shared with neighbors.  
- **Fiber (GPON/EPON):** Light-based, symmetrical, 1–10 Gbps.

#### Operation
- Auth via **PPPoE**  
- NAT/PAT for internal users  
- Usually dynamic public IPs  

**Pros:** Cheap, fast bursts, easy setup  
**Cons:** Shared, distance-limited, variable latency


### WAN Trio Comparison

| Tech | Speed/Symmetry | Cost | Reliability | Use Case |
|------|----------------|------|-------------|-----------|
| **MPLS** | 10M–100G (Sym) | High | High + QoS | Enterprise VPNs |
| **Leased Line** | 1M–10G (Sym) | $$$ | Excellent | Corporate HQ Links |
| **Broadband** | 10M–1G (Asym) | Low | Variable | Home / SOHO |

 **Short Explnation**

- **MPLS** = Smart cloud (speed + QoS)  
- **Leased Line** = Private jet (dedicated & secure)  
- **Broadband** = City bus (cheap, shared)  


# References

**Day 1** - [ACL](https://claude.ai/public/artifacts/bd93a197-c4e7-4055-8fb8-244f36c6d823)  

**Day 2** - [LAN Switching](https://claude.ai/public/artifacts/c07e6c2a-f9ae-4abd-a263-adb67b666bc9)  

**Day 3** - [WAN ](https://claude.ai/public/artifacts/376a8e93-7bdb-4cc1-9ab0-057fe128fc43) 


