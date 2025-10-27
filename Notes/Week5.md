#  Networking Internship Notes: OSPF, EIGRP, and BGP Days

##  Day 1: OSPF – Link-State Powerhouse

**OSPF is a dynamic routing protocol used inside a single organization or network to help routers automatically find the best path for sending data. Suppose a company has many routers spread across different departments like Admin, HR, and IT. Each router needs to know how to reach the others efficiently. Doing this manually would be time-consuming and prone to errors, especially if a link goes down or a new router is added. OSPF solves this by automatically discovering routes and updating them whenever the network changes. It builds a complete map of the network using something called a Link-State Database (LSDB). Then, each router uses a mathematical formula called the Shortest Path First (SPF) algorithm to calculate the most efficient route. In simple terms, OSPF works like Google Maps for routers — it always looks for the shortest, most reliable route and updates the map automatically if roads (links) change.

###  Core Specs
- **Type:** IGP (Link-State)  
- **Metric:** Cost = 1 / Bandwidth  
- **Best For:** Large, dynamic enterprise networks  

###  Why It’s Boss
- **Fast Convergence:** Sub-second reroutes  
- **Hierarchical Design:** Areas (Area 0 = Backbone)  
- **Scalable:** Handles thousands of routers  
- **Supports VLSM/CIDR:** Efficient IP usage  
- **Multicast Updates:** 224.0.0.5 & 224.0.0.6  
- **Authentication:** MD5 support  

**Lab:** 4-router mesh — pulled a cable; ping barely blinked.  
(RIP would’ve died crying )

###  OSPF Workflow
1. **Neighbor Discovery:** Hellos (every 10s) → adjacency formed  
2. **DBD Exchange:** Summary of LSAs  
3. **LSDB Flood:** Complete topology sync  
4. **SPF Calculation:** Dijkstra builds routing table  

###  OSPF Areas
| Type | Description |
|------|--------------|
| **Area 0 (Backbone)** | Central hub, all other areas connect here |
| **Standard Area** | Full LSAs exchanged |
| **Stub Area** | Blocks externals, adds default route |
| **Totally Stubby** | Only default routes allowed |
| **NSSA** | Like Stub + limited external routes |

**Lab:** Stub area = quicker convergence, lighter load.

###  OSPF Packet Types
| Type | Purpose |
|------|----------|
| **Hello** | Maintain neighbors |
| **DBD** | LSDB summary |
| **LSR** | Request missing LSAs |
| **LSU** | Send LSA data |
| **LSAck** | Confirm receipt |


###  Authentication Modes
- **Null:** No auth (lab only)  
- **Plain Text:** Weak  
- **MD5:** Secure & standard  

 **Ref:** Day 1 OSPF Lab — Multi-area next?


##  Day 2: EIGRP – Cisco Hybrid Hustle

**EIGRP is a Cisco-developed dynamic routing protocol designed to share routing information automatically between routers within a network. It improves on older protocols like RIP, which only counted the number of hops between routers, by adding intelligence. EIGRP considers multiple factors such as bandwidth, delay, reliability, and load to decide the best route. Think of it like comparing two roads: one is short but full of traffic, and the other is longer but faster and smoother. EIGRP will choose the overall best one by analyzing these details. It also keeps backup routes ready using an algorithm called DUAL (Diffusing Update Algorithm), so if one path fails, the network instantly switches to another without delay. Because of its speed and stability, EIGRP became very popular in Cisco-based enterprise networks. In short, it’s a smart and efficient protocol that finds the best routes and always keeps an alternate plan ready

### Specs
- **Type:** Advanced Distance-Vector (DUAL)  
- **Metric:** Bandwidth + Delay (optionally reliability/load)  
- **Vendor:** Cisco (partially open RFC 7868)

###  Highlights
- **Fast Convergence:** Feasible Successors = instant backup  
- **Loop-Free:** Thanks to feasibility condition  
- **Efficient:** Partial updates (multicast 224.0.0.10)  
- **Supports VLSM/CIDR**  
- **Unequal Load Balancing:** Up to 32 paths  

**Lab:** Ping held mid-failure — FS took over instantly 


###  EIGRP Flow
1. **Neighbors:** Hellos (5s on LAN), K-values must match  
2. **Topology Table:** Lists all routes (Successor + Feasible Successor)  
3. **DUAL Algorithm:** Chooses best & backup paths  
4. **RIB:** Successors move to routing table  

`show ip eigrp topology` → reveals FS metrics.


###  EIGRP Metric Formula
- **Bandwidth:** 10^7 / min_kbps  
- **Delay:** Sum of interface delays (in tens of µs)  
- **Default Weights:** K1=1, K3=1  

**Lab:** Adjusted K-values to favor stable paths.

###  EIGRP Packets
| Type | Role |
|------|------|
| Hello | Neighbor discovery |
| Update | Routing info |
| Query | Route request |
| Reply | Query response |
| ACK | Acknowledgment |


###  Authentication
- **MD5 Keychains:** Prevent spoofed updates  

 **Ref:** Day 2 EIGRP — OSPF’s speedy cousin, Cisco style.


##  Day 3: BGP – The Internet’s Path Whisperer

**BGP is the main routing protocol that powers the entire Internet. It connects large networks, such as Internet Service Providers (ISPs), companies, or universities, which are called Autonomous Systems (AS). Each AS manages its own internal network, but they all need a way to share routing information with one another so data can travel across the world. That’s where BGP comes in. It works like an international postal system — each AS tells others which destinations it can reach, and routers decide how to forward data based on policies, cost, or reliability. Unlike OSPF, BGP doesn’t always choose the shortest path. Instead, it chooses the best path according to business or routing policies. For example, if Jio and Airtel both have routes to the USA, your ISP might select Airtel’s route because it’s cheaper or more reliable, even if it’s slightly longer. BGP is slower to update routes, but it’s extremely stable and designed to handle the massive scale of the global Internet.


###  Core Specs
- **Type:** EGP (Path-Vector)  
- **Metric:** None — uses attributes (Local Pref, AS_PATH, MED)  
- **Scope:** Inter-AS (Internet-wide)  


###  Why It Matters
- **Global Backbone:** Handles ~900K+ prefixes  
- **Policy Control:** Routing decisions = admin rules, not speed  
- **Scalable:** Incremental updates  
- **Loop Avoidance:** AS_PATH checks  
- **iBGP/eBGP Split:** iBGP (internal peers), eBGP (external peers)  
- **Convergence:** Slower but more stable  

**Lab:** ISP peering simulation — eBGP up on TCP 179.  
Path flaps smoothed by hold timers.


###  BGP Route Workflow
1. **Session Setup:** TCP port 179, `OPEN` + `KEEPALIVE`  
2. **Update Exchange:** Prefixes (NLRI) + attributes  
3. **Decision Process:** 13-step best-path rules (Local Pref → AS_PATH → MED → …)  
4. **Scaling Tools:** Route Reflectors & Confederations  
5. **Attributes:**
   - **Well-Known Mandatory:** AS_PATH, ORIGIN  
   - **Discretionary:** Local Pref, MED, Community  

**Lab:** Tweaked Local Pref — preferred path shifted instantly.  
Added `no-export` community to stop external leaks.


###  BGP Message Types
| Message | Purpose |
|----------|----------|
| **OPEN** | Start session (AS info, timers) |
| **UPDATE** | Advertise or withdraw routes |
| **KEEPALIVE** | Maintain session |
| **NOTIFICATION** | Error or shutdown alert |


###  Security
- **MD5 TCP Auth:** Protects BGP sessions  
- **RPKI:** Validates prefixes (stops route hijacks)  

**Takeaway:** BGP = Internet diplomat — stable, policy-driven, essential.  
**Downside:** Complex and slow, but unbeatable globally.


##  Trio Throwdown: OSPF vs EIGRP vs BGP

| Aspect | OSPF | EIGRP | BGP |
|--------|------|-------|-----|
| **Type** | IGP (Link-State) | IGP (Adv DV) | EGP (Path-Vector) |
| **Scope** | Single AS | Single AS | Multi-AS |
| **Metric** | Cost (BW) | BW + Delay | Attributes |
| **Convergence** | Fast (sec) | Fastest (<1s) | Slow (mins) |
| **Scale** | Large | Large | Massive |
| **Updates** | LSAs Flood | Partial Multicast | Incremental |
| **Loop Avoidance** | SPF Tree | Feasibility | AS_PATH |
| **Vendor** | Open | Cisco | Open |
| **Best For** | Enterprise internal | Cisco internal | ISP / Global |
| **Complexity** | Medium | Easy | High |
| **Lab Highlight** | Area re-route | FS recovery | Policy tweak |

###  Short Explanation

- **OSPF:** Structured & scalable — corporate networks  
- **EIGRP:** Cisco’s speed demon — fast failover  
- **BGP:** Internet’s diplomat — massive scale & policy control  

**Together, they power every layer of routing — from small LANs to the global Internet.**  

# References

**Day 1** - [OSPF](https://claude.ai/public/artifacts/fbf70cac-6f1a-41cf-adcc-6336e3136ab5?fullscreen=true)  
**Day 2** - [EIGRP](https://claude.ai/public/artifacts/c030298c-25c3-490e-a1ff-eb03eda1f418?fullscreen=true)  
**Day 3** - [BGP](https://claude.ai/public/artifacts/819e1cd3-57ee-4398-9446-513c3cce9597)

