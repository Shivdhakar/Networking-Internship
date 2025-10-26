# Switches: L2 vs L3, VLANs, Trunks, and STP Notes

## What’s a Switch?
Picture this: A switch is basically a smart box that hooks up a bunch of devices—your laptop, office printer, server rack—in the same local network (think company LAN). Old-school hubs just blast data everywhere, wasting bandwidth and slowing things down. But a switch? It peeks at the destination (like checking the address on an envelope) and sends the packet only to the right device. Boom—faster speeds, less junk traffic, and the network hums along. We tested this in Packet Tracer; without it, pings were lagging like crazy.

## Layer 2 (L2) Switches: The Basics Guy
L2 switches hang out at the Data Link layer (Layer 2 of OSI—remember that from last week?). They use MAC addresses (those unique hardware IDs, like 00:1A:2B:3C:4D:5E) to forward frames within the same network.

- **What it does:** Learns MACs from incoming traffic (builds a table called CAM), then zips data to the exact port. Super efficient for local chit-chat.
- **Where it shines:** Small setups, like a team room with 10 PCs. Connect 'em all, and everyone's sharing files without drama.
- **The catch:** It can't hop between different networks (like from your dept to sales). If you need that, you're stuck—data stops at the LAN border. In our lab, trying to ping across subnets? Total fail until we added routing.

Pro tip: Most home routers have a built-in L2 switch for your WiFi devices. That's why your smart TV doesn't flood your phone with Netflix data.

## Layer 3 (L3) Switches: The Multitasker
Now, L3 switches level up to the Network layer (Layer 3). They handle IP addresses (like 192.168.1.10) for routing, while still doing all the L2 switching magic.

- **What it does:** Switches locally *and* routes between subnets/VLANs. It's like a router on steroids—hardware-accelerated, so no software bottlenecks.
- **When to grab one:** Big offices or campuses. Say, 200+ users split into depts; L3 lets HR talk to Finance without a separate router hogging space.
- **Trade-offs:** A tad pricier and uses more power, but in our sim, it cut latency by half compared to chaining L2s with a router.

We configured one in class—assigned IPs, set up routes, and watched inter-VLAN pings fly. Felt like wizardry.

## L2 vs L3: Head-to-Head
Here's a quick table I sketched during break. Makes comparing 'em a breeze.

| Feature          | L2 Switch                          | L3 Switch                              |
|------------------|------------------------------------|----------------------------------------|
| OSI Layer        | Data Link (Layer 2)                | Network (Layer 3)                      |
| Addresses Used   | MAC (hardware IDs)                 | IP (logical addresses)                 |
| Core Job         | Local traffic switching in one LAN | Switching + routing across networks    |
| Speed/Complexity | Blazing fast, dead simple          | Fast, but juggles more (routing logic) |
| Best For         | Small office, single subnet        | Enterprise with VLANs/subnets          |
| Cost             | Cheaper, entry-level               | More bucks, but scales big             |

Bottom line: Start with L2 for basics; upgrade to L3 when your network grows legs.

## VLANs and Trunks: Keeping Things Organized
Networks can get messy fast—broadcast storms, security leaks. Enter VLANs and trunks to tame the beast.

### VLANs: Virtual Neighborhoods
VLAN (Virtual LAN) is like drawing invisible fences on your physical switch. You group devices logically by role (e.g., all marketing laptops in one "virtual net"), even if they're scattered across ports or switches.

- **Why bother?** Each VLAN is its own bubble—broadcasts (like ARP yells) stay inside, cutting noise. Plus, security: Finance VLAN can't snoop on IT without permission.
- **How it works:** Assign ports to VLAN IDs (e.g., VLAN 10 for Sales). Devices in VLAN 10 think they're alone, even on a shared switch.
- **Real talk:** Without routing (L3 switch/router), VLANs are islands—no cross-talk. In lab, we split a 24-port switch into 3 VLANs; traffic dropped 70% on broadcasts.

Example from our company sim:  
- VLAN 10: HR (10 users, sensitive payroll stuff).  
- VLAN 20: Dev Team (20 coders, high bandwidth).  
- VLAN 30: Guests (WiFi access, firewalled).  
HR can't accidentally flood devs with HR memos.

### Trunks: The VLAN Highway
Trunk links are special cables/ports that shuttle *multiple* VLANs over one connection (switch-to-switch or switch-to-router). Without 'em, you'd need a wire per VLAN—cable salad!

- **The magic:** IEEE 802.1Q adds a tiny tag (VLAN ID) to each Ethernet frame. Switch reads the tag and drops it into the right VLAN bucket.
- **Setup:** Enable trunk mode on ports, specify allowed VLANs (e.g., "trunk VLANs 10,20"). Native VLAN (untagged) for legacy stuff.
- **Why it rocks:** Saves ports and cabling. In our multi-switch lab, one trunk carried 5 VLANs—clean and scalable.

Example: Two switches, A and B. Trunk between 'em carries VLAN 10 (HR) and 20 (IT). HR laptop on A reaches HR printer on B seamlessly.

### VLAN vs Trunk: Don't Mix 'Em Up
Quick diff table—VLAN is the group, trunk is the bridge.

| Feature              | VLAN (Virtual Network)                  | Trunk (VLAN Carrier)                    |
|----------------------|-----------------------------------------|-----------------------------------------|
| What It Is           | Logical split of physical ports/devices | Special link for multi-VLAN traffic     |
| Scope                | One switch or domain                    | Between switches/devices                |
| Broadcast Handling   | Each VLAN = separate domain             | Carries multiple domains over one wire  |
| Tagging              | N/A (access ports untagged)             | 802.1Q tags frames                      |
| Example              | VLAN 10 = All sales PCs                 | Trunk port linking Switch1 to Switch2   |

Pro: VLANs + trunks = flexible, secure networks without rewiring.

## Spanning Tree Protocol (STP): Loop Buster
Redundant links sound great (backup paths!), but they create loops—data circles forever, crashing the network. STP (IEEE 802.1D) is the cop that shuts down extras, keeping Layer 2 loop-free.

### STP Basics
It builds a single active tree topology: One root, no cycles. Uses BPDUs (Bridge Protocol Data Units) for switches to chat and decide.

- **Root Bridge:** The "king" switch—lowest Bridge ID (priority + MAC). Elect it first (set low priority on a central switch).
- **Ports Roles:**  
  - Root Port (RP): Non-root switch's best shot to root (lowest cost).  
  - Designated Port (DP): Forwards on a segment (one per link).  
  - Blocked: Stands by, no forwarding (prevents loops).
- **Path Cost:** Based on speed (e.g., 10Gbps = cost 2, 100Mbps = 19). Lower = preferred.
- **States (Old STP):** Blocking (listen), Listening (elect), Learning (build table), Forwarding (go time). Takes 30-50s to converge—yawn.

RSTP (Rapid STP) fixes that: Faster handshakes, under 5s convergence.

### How STP Plays Out
1. **Election:** All switches yell BPDUs. Lowest BID wins root.
2. **Root Ports:** Everyone picks their fastest path to root.
3. **Designated Ports:** Per segment, the root-closest port forwards.
4. **Blocking:** Others chill—ready to activate if link fails.
5. **Convergence:** Timers tick (Max Age 20s, Hello 2s), topology locks in.

If a link dies? BPDUs stop, blocked port flips to forwarding quick.

### Real-World Examples
- **Triangle Setup:** Switches A-B-C, plus A-C link. STP picks A as root, blocks A-C. Traffic A→B→C. If B fails, unblock A-C.
- **Access Layer:** End switch with dual uplinks to core switches. One uplink DP (active), other blocked. Failover? Instant switch.

In lab: We looped three switches—flood city until STP kicked in. Blocked port saved the day.

### Handy Cisco Commands
We ran these on our 2960s—gold for troubleshooting.

- `show spanning-tree` – Full STP deets, root, ports.  
- `show spanning-tree root` – Who's boss and paths.  
- `show spanning-tree brief` – Port roles/states at a glance.  
- `spanning-tree vlan 1 priority 4096` – Make this switch root candidate (lower number = better).  
- `spanning-tree portfast` – Skip Listening/Learning on access ports (edge devices only!).

Wrapping up: Switches are network MVPs. L2 for simple, L3 for smart growth. VLANs segment, trunks connect, STP prevents meltdowns. Can't wait to wire this in a real rack. Day's learning: Redundancy without loops = happy admins. 
