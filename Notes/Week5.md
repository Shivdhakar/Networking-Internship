#  Networking Internship Notes: OSPF, EIGRP, and BGP Days

##  Day 1: OSPF – Link-State Powerhouse

**OSPF (Open Shortest Path First)** — the IGP beast for a single AS (company network).  
A **link-state protocol** where routers share full link maps, and Dijkstra’s algorithm finds the shortest path (graph flashback!).  
Defined in **RFC 2328**, fully vendor-neutral.

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

---

###  OSPF Workflow
1. **Neighbor Discovery:** Hellos (every 10s) → adjacency formed  
2. **DBD Exchange:** Summary of LSAs  
3. **LSDB Flood:** Complete topology sync  
4. **SPF Calculation:** Dijkstra builds routing table  

---

###  OSPF Areas
| Type | Description |
|------|--------------|
| **Area 0 (Backbone)** | Central hub, all other areas connect here |
| **Standard Area** | Full LSAs exchanged |
| **Stub Area** | Blocks externals, adds default route |
| **Totally Stubby** | Only default routes allowed |
| **NSSA** | Like Stub + limited external routes |

**Lab:** Stub area = quicker convergence, lighter load.

---

###  OSPF Packet Types
| Type | Purpose |
|------|----------|
| **Hello** | Maintain neighbors |
| **DBD** | LSDB summary |
| **LSR** | Request missing LSAs |
| **LSU** | Send LSA data |
| **LSAck** | Confirm receipt |

---

###  Authentication Modes
- **Null:** No auth (lab only)  
- **Plain Text:** Weak  
- **MD5:** Secure & standard  

 **Ref:** Day 1 OSPF Lab — Multi-area next?

---

##  Day 2: EIGRP – Cisco Hybrid Hustle

**EIGRP (Enhanced Interior Gateway Routing Protocol)** — Cisco’s hybrid mix of distance-vector and link-state ideas.  
Uses the **DUAL** algorithm for ultra-fast recovery and loop-free paths.

### Specs
- **Type:** Advanced Distance-Vector (DUAL)  
- **Metric:** Bandwidth + Delay (optionally reliability/load)  
- **Vendor:** Cisco (partially open RFC 7868)

---

###  Highlights
- **Fast Convergence:** Feasible Successors = instant backup  
- **Loop-Free:** Thanks to feasibility condition  
- **Efficient:** Partial updates (multicast 224.0.0.10)  
- **Supports VLSM/CIDR**  
- **Unequal Load Balancing:** Up to 32 paths  

**Lab:** Ping held mid-failure — FS took over instantly 

---

###  EIGRP Flow
1. **Neighbors:** Hellos (5s on LAN), K-values must match  
2. **Topology Table:** Lists all routes (Successor + Feasible Successor)  
3. **DUAL Algorithm:** Chooses best & backup paths  
4. **RIB:** Successors move to routing table  

`show ip eigrp topology` → reveals FS metrics.

---

###  EIGRP Metric Formula
- **Bandwidth:** 10^7 / min_kbps  
- **Delay:** Sum of interface delays (in tens of µs)  
- **Default Weights:** K1=1, K3=1  

**Lab:** Adjusted K-values to favor stable paths.

---

###  EIGRP Packets
| Type | Role |
|------|------|
| Hello | Neighbor discovery |
| Update | Routing info |
| Query | Route request |
| Reply | Query response |
| ACK | Acknowledgment |

---

###  Authentication
- **MD5 Keychains:** Prevent spoofed updates  

 **Ref:** Day 2 EIGRP — OSPF’s speedy cousin, Cisco style.

---

##  Day 3: BGP – The Internet’s Path Whisperer

**BGP (Border Gateway Protocol)** — the global routing boss, controlling how data moves between ISPs and large networks.  
**Path-vector protocol** — focuses on policies, not distances.  
Defined in **RFC 4271**, current version: **BGPv4**.

---

###  Core Specs
- **Type:** EGP (Path-Vector)  
- **Metric:** None — uses attributes (Local Pref, AS_PATH, MED)  
- **Scope:** Inter-AS (Internet-wide)  

---

###  Why It Matters
- **Global Backbone:** Handles ~900K+ prefixes  
- **Policy Control:** Routing decisions = admin rules, not speed  
- **Scalable:** Incremental updates  
- **Loop Avoidance:** AS_PATH checks  
- **iBGP/eBGP Split:** iBGP (internal peers), eBGP (external peers)  
- **Convergence:** Slower but more stable  

**Lab:** ISP peering simulation — eBGP up on TCP 179.  
Path flaps smoothed by hold timers.

---

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

---

###  BGP Message Types
| Message | Purpose |
|----------|----------|
| **OPEN** | Start session (AS info, timers) |
| **UPDATE** | Advertise or withdraw routes |
| **KEEPALIVE** | Maintain session |
| **NOTIFICATION** | Error or shutdown alert |

---

###  Security
- **MD5 TCP Auth:** Protects BGP sessions  
- **RPKI:** Validates prefixes (stops route hijacks)  

**Takeaway:** BGP = Internet diplomat — stable, policy-driven, essential.  
**Downside:** Complex and slow, but unbeatable globally.

 **Ref:** Day 3 BGP — World-stage routing champ.

---

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

---

###  Summary

- **OSPF:** Structured & scalable — corporate networks  
- **EIGRP:** Cisco’s speed demon — fast failover  
- **BGP:** Internet’s diplomat — massive scale & policy control  

**Together, they power every layer of routing — from small LANs to the global Internet.**  

# References

**Day 1** - [OSPF](https://claude.ai/public/artifacts/fbf70cac-6f1a-41cf-adcc-6336e3136ab5?fullscreen=true)  
**Day 2** - [EIGRP](https://claude.ai/public/artifacts/c030298c-25c3-490e-a1ff-eb03eda1f418?fullscreen=true)  
**Day 3** - [BGP](https://claude.ai/public/artifacts/819e1cd3-57ee-4398-9446-513c3cce9597)

