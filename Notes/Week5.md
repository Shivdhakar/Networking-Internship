# Networking Internship Notes: OSPF and EIGRP Days

---

## Day 1: OSPF – The Link-State Brainiac

OSPF (Open Shortest Path First) is this powerhouse IGP for inside one autonomous system (AS — like your company's whole net). It's link-state, meaning routers share full maps of links, not just rumors like distance-vector. It calculates shortest paths with Dijkstra's algorithm (that graph wizardry from college). RFC 2328 standard, open to all — not Cisco-locked.

**Why it slays**
- **Type:** IGP, link-state  
- **Metric:** Cost (inverse bandwidth — faster link = lower cost)  
- **Vibe:** Scales huge, converges in seconds, loves hierarchies  

### Standout Perks
- **Fast Convergence:** Change a link? Everyone knows quickly  
- **Areas for Organization:** Breaks big networks into zones (Area 0 = backbone)  
- **Scalable:** Works well with thousands of routers  
- **VLSM and CIDR Support:** Efficient IP usage  
- **Multicast Updates:** Uses 224.0.0.5 and 224.0.0.6  
- **Security:** Supports authentication to prevent fake updates  

In the lab, we built a four-router OSPF network. Disconnected one link and saw routes update in under a second. RIP would have taken much longer.

### How OSPF Works
1. **Neighbor Discovery:** Routers send hello packets every 10 seconds. If parameters match, they become neighbors.  
2. **Database Exchange:** Routers share summaries of link-state info through DBD packets.  
3. **LSDB Synchronization:** Routers flood LSAs so every router has the same network map.  
4. **SPF Calculation:** Dijkstra's algorithm runs to create shortest path trees and updates routing tables.  

### OSPF Areas
Areas help keep things organized. The backbone (Area 0) connects all other areas.

- **Backbone (Area 0):** Main communication center  
- **Standard Area:** Normal routing with full LSAs  
- **Stub Area:** No external routes, only internal  
- **Totally Stubby Area:** Removes extra LSAs, lightest load  
- **NSSA:** Allows some external routes but with limits  

We created a stub area in the lab, which improved convergence speed.

### OSPF Packet Types
| Packet Type | Purpose |
|--------------|----------|
| Hello | Maintains neighbor relationships |
| DBD | Shares database summaries |
| LSR | Requests missing LSAs |
| LSU | Sends complete LSA information |
| LSAck | Acknowledges receipt |

### Authentication
- **Null:** No security, for labs only  
- **Simple Text:** Password visible, not secure  
- **MD5:** Secure hash-based authentication (recommended)

**Ref:** Day 1 OSPF Hands-On — OSPF feels like the network has full awareness of itself. Next time, planning multi-area setups.

---

## Day 2: EIGRP – Cisco's Hybrid Speedster

EIGRP (Enhanced Interior Gateway Routing Protocol) is Cisco's advanced distance-vector protocol. It blends distance-vector and link-state features — hybrid design for fast and reliable routing. Originally Cisco-only, but now partially open under RFC 7868.

**Details**
- **Type:** Advanced Distance Vector (DUAL engine)  
- **Metric:** Combines bandwidth and delay (optionally reliability and load)  
- **Best For:** Cisco routers and enterprise networks  

### Features
- **Rapid Convergence:** DUAL ensures instant recovery using feasible successors  
- **Loop-Free Operation:** Uses feasible condition to avoid loops  
- **Partial Updates:** Only affected routers get changes  
- **VLSM & CIDR Support:** Efficient addressing  
- **Unequal Load Balancing:** Multiple paths with different costs  
- **Multicast Updates:** Uses 224.0.0.10  

**Lab Test:** Broke a link while pinging — failover happened in less than a second thanks to feasible successors.

### How EIGRP Works
1. **Neighbor Formation:** Routers exchange hellos every 5 seconds on LAN and agree on K-values  
2. **Topology Table:** Stores all possible routes including successors and feasible successors  
3. **DUAL Algorithm:** Calculates best path and queries neighbors if no backup available  
4. **Routing Table:** Adds only the best successor route  

Command:  
```bash
show ip eigrp topology
