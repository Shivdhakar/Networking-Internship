# Networking Internship Notes STP, Routing, and RIP Days

---

## Day 1 Spanning Tree Protocol STP – Avoiding Infinite Loops

STP is a key protocol that prevents loops in Ethernet networks. It follows IEEE 802.1D standards and ensures there are no endless data cycles that could flood and crash the network.

### Why We Use STP
- Stops loops at Layer 2 to prevent data from endlessly circulating.  
- Keeps backup links ready for redundancy.  
- Automatically enables or disables ports to keep network traffic smooth.  

In the lab, connecting three switches in a loop without STP caused ping failures. After enabling STP, everything stabilized.

### How STP Works
STP chooses one switch as the Root Bridge and calculates the shortest path to it. Any extra links are blocked to avoid loops.

Key Steps
1. Root Bridge Election Each switch shares its Bridge ID which includes priority and MAC address. The one with the lowest ID becomes the root.  
2. Path Cost Each link has a cost based on speed. Faster links mean lower cost.  
3. Port Roles  
   - Root Port Best path to the root bridge on non-root switches.  
   - Designated Port The main forwarding port for a network segment.  
   - Blocked Port A backup that stays idle until needed.  

### Port States
Ports transition through several stages  
- Blocking Listens but does not forward data.  
- Listening Starts BPDU exchange for election.  
- Learning Learns MAC addresses but no forwarding yet.  
- Forwarding Sends and receives frames.  
- Disabled Not active at all.  

Traditional STP takes 30 to 50 seconds to converge. RSTP reduces it to less than 5 seconds.

### STP Versions

| Type | Description |
|------|--------------|
| STP 802.1D | Original standard, slow convergence |
| RSTP 802.1w | Faster recovery and response |
| MSTP 802.1s | Supports multiple VLANs in one tree |
| PVST Plus | Cisco version, separate STP per VLAN |

### Benefits
- Prevents loops and broadcast storms  
- Provides redundancy  
- Adjusts automatically to topology changes  
- Improves reliability  

### Example Triangle Topology
With three switches A, B, and C connected in a loop, packets can travel endlessly. STP selects A as the root and blocks one redundant link, creating a loop-free structure. If a link fails, STP reactivates the backup within seconds.

Reference Day 1 STP session completed successfully. Planning to try RSTP next.

---

## Day 2 Routing Basics – How Data Finds Its Way

Routing operates at Layer 3 of the OSI model. It determines the best path for data packets to reach their destination across networks.

### Real World Example
Think of packets as cars, routers as intersections, and routing tables as maps. Just like a GPS avoids traffic jams, routers choose the fastest or most efficient route for data.

### Core Concepts
- Router Directs packets based on their destination IP.  
- Routing Table Stores destination networks, next hops, and metrics.  

Example entry  
- Destination IP 192.168.1.0  
- Subnet Mask 255.255.255.0  
- Next Hop 10.0.0.1  
- Interface Gig0 or 1  
- Metric Number of hops or cost  

If no route matches, the packet is dropped.

### Types of Routing
1. Static Routing Manually configured routes, stable but not scalable.  
2. Dynamic Routing Routers automatically share and update route information using protocols.  

### Popular Routing Protocols

| Protocol | Type | Description |
|-----------|------|-------------|
| RIP | Distance Vector | Simple, uses hop count with a max of 15 |
| OSPF | Link State | Builds full network map for efficient routing |
| EIGRP | Hybrid | Combines distance vector and link state features |
| BGP | Path Vector | Used for routing between organizations or ISPs |

### Routing Process
1. Packet enters router.  
2. Destination IP is checked.  
3. Best route is selected based on metrics.  
4. Packet is sent to next hop or interface.  
5. Process repeats until destination is reached.  

### Advantages
- Enables communication between different networks.  
- Provides backup paths and auto recovery.  
- Supports internet scale communication.  
- Can apply security filters using ACLs.  

Example A company with offices in Bangalore and Delhi connected both LANs using OSPF. The result was seamless communication between sites.

Reference Day 2 Routing Lab. Routing tables now make complete sense.

---

## Day 3 Intra and Interdomain Routing and RIP Protocol

Dynamic routing can be divided into two major types Intra and Interdomain routing.

### Intra vs Interdomain

- **Intradomain IGP** Operates within one organization’s network using protocols like RIP, OSPF, or EIGRP.  
- **Interdomain EGP** Connects multiple organizations or ISPs using BGP.  

Analogy Intradomain is like local city traffic, while Interdomain is the highway between cities.

Small organizations use IGP while ISPs rely on BGP for larger control.

---

### RIP Routing Information Protocol

RIP is an intradomain distance vector protocol. It calculates the best path based on hop count. The maximum hop limit is 15; anything beyond that is unreachable.

**Key Features**
- Metric based on hop count only.  
- Updates sent every 30 seconds.  
- Uses Bellman Ford algorithm for path calculation.  

RIP does not consider bandwidth or delay—just hop numbers.

---

### RIP Version Comparison

| Feature | RIPv1 | RIPv2 |
|----------|--------|--------|
| Classful | Yes | No supports VLSM |
| Subnet Mask Info | Not included | Included in updates |
| Update Type | Broadcast | Multicast to 224.0.0.9 |
| Authentication | None | Supports text or MD5 |
| VLSM Support | No | Yes |

RIPv2 is widely used because it is more efficient and secure.

---

### How RIP Works
1. Each router knows its directly connected networks.  
2. Every 30 seconds, routers share their tables with neighbors.  
3. Routers compare paths and select the lowest hop count.  
4. Split horizon and poison reverse prevent routing loops.  
5. Routes are updated continuously.  

**Timers**
- Update 30 seconds  
- Invalid 180 seconds  
- Holddown 180 seconds  
- Flush 240 seconds  

If a route update is missed, the route eventually expires and is removed.

---

### When to Use RIP
Best for small networks with fewer than 15 routers.  
Benefits  
- Simple to configure  
- Low resource usage  
- Ideal for small branch networks  

Example A retail company with multiple stores uses RIP to connect routers across branches. The protocol automatically shares route info without complex setup.

For larger networks, OSPF is preferred due to RIP’s hop limit.

Reference Day 3 RIP and Routing discussion completed. Next goal OSPF hands on configuration.
