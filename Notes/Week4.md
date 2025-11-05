# Networking Internship

## Day 1 Spanning Tree Protocol STP – Avoiding Infinite Loops

STP is a network protocol used to prevent loops in a Layer 2 (switch-based) network. When multiple switches are connected together in a network, sometimes redundant links are added for backup. These backup paths are useful for reliability, but they can also create loops — meaning data packets keep circulating endlessly between switches. This can slow down or even crash the entire network. STP solves this by automatically detecting and blocking extra paths that could cause loops, leaving only one active path for communication. If the main path fails, STP quickly activates one of the blocked backup paths to keep the network running smoothly. It works by choosing one switch as the Root Bridge (like the main reference point) and then calculating the best path to it. In short, STP ensures that switches are connected efficiently without creating endless data loops, keeping the network stable and reliable.

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

## Day 2 Routing Basics – How Data Finds Its Way

Routing is the process of finding the best path for data to travel from one network to another. Routers are the devices responsible for routing—they act like traffic managers that guide data packets toward their destination. Each router stores information in a routing table, which tells it which path or next hop to use for specific destinations. There are two main types of routing: Static Routing and Dynamic Routing. In static routing, routes are manually set by a network administrator, which works well for small and stable networks. In dynamic routing, routers automatically share information and update their routes using routing protocols like OSPF, EIGRP, or BGP. Routing is essential for communication between different networks, ensuring that data takes the most efficient path and reaches its target safely. Without routing, computers in different networks or locations wouldn’t be able to talk to each other.

### Real World Example
Think of packets as cars, routers as intersections, and routing tables as maps. Just like a GPS avoids traffic jams, routers choose the fastest or most efficient route for data.

### Core Concepts
- Router Directs packets based on their destination IP.  
- Routing Table Stores destination networks, next hops, and metrics.  


## Types of Routing

### Static Routing
Static routing means we **manually set the route** in the router.  
The router does not learn automatically — we have to enter the path ourselves.

**Simple meaning:**  
We give the router a fixed path, like choosing directions manually on Google Maps.

**Best for:** Small networks  
**Drawback:** Not good for big networks because updating routes manually takes time.

---

### Dynamic Routing
Dynamic routing means routers **automatically learn and share routes** with each other.  
They select the best path based on network conditions.

**Simple meaning:**  
Routers act smart — they talk to each other and find the best route automatically.

**Best for:** Medium and large networks  
**Advantage:** Auto updates if network changes.

---

### Comparison

| Feature | Static Routing | Dynamic Routing |
|--------|----------------|----------------|
| Configuration | Manual | Automatic |
| Best Use | Small network | Big network |
| Updates | No auto update | Automatically updates |
| Control | Full control | Router decides the best path |


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

---

# [Click here to view image Types of Routing ](../Asset/routing.png)

---



## Day 3 Intra and Interdomain Routing and RIP Protocol

Dynamic routing can be divided into two major types Intra and Interdomain routing.

### Intra vs Interdomain

- **Intradomain IGP**
- Interdomain routing is the process of exchanging routing information between different organizations or networks, known as Autonomous Systems (AS). Each AS is a large network managed by a single organization, such as an Internet Service Provider (ISP), a university, or a large company. Since the Internet is made up of thousands of these independent systems, they need a way to communicate and share route information so data can travel from one network to another across the world. This is where Interdomain Routing comes in. The main protocol used for this purpose is BGP (Border Gateway Protocol), which acts like the Internet’s postal service, deciding how data should move between different networks. Interdomain routing focuses on policy-based routing rather than just shortest paths. For example, an ISP may choose a route based on cost, reliability, or a business agreement with another provider. In short, Interdomain Routing connects big networks together and forms the backbone of the Internet.
-   
- **Interdomain EGP**
- Intradomain routing happens within a single organization or Autonomous System. Unlike interdomain routing, which connects large, separate networks, intradomain routing focuses on managing traffic inside one company or internal network. The goal is to make sure all devices within that network can communicate efficiently and automatically find the best path for data. Common Intradomain Routing Protocols include OSPF (Open Shortest Path First), EIGRP (Enhanced Interior Gateway Routing Protocol), and RIP (Routing Information Protocol). These protocols help routers inside the organization learn about each other’s connections and update routes when changes happen, such as a link failure. For example, in a company with multiple departments connected by routers, intradomain routing ensures data can move smoothly from the HR router to the Finance router without needing any manual configuration. In simple words, intradomain routing manages internal communication, while interdomain routing connects that internal network to the outside world. 

Analogy Intradomain is like local city traffic, while Interdomain is the highway between cities.

Small organizations use IGP while ISPs rely on BGP for larger control.

### RIP Routing Information Protocol

RIP is one of the oldest and simplest dynamic routing protocols used in networks. It helps routers automatically learn and share routes with each other so that data can reach the right destination. RIP works by counting hops — the number of routers data must pass through to reach its target. The path with the fewest hops is chosen as the best route. However, RIP has a limitation: it can only count up to 15 hops, which means it’s best suited for small networks. Every 30 seconds, routers using RIP send updates to their neighbors to share their routing tables. While this makes RIP easy to configure, it also means it converges slowly compared to newer protocols like OSPF or EIGRP. Despite being older, RIP is still useful for learning and understanding the basic concepts of dynamic routing.

**Key Features**
- Metric based on hop count only.  
- Updates sent every 30 seconds.  
- Uses Bellman Ford algorithm for path calculation.  

RIP does not consider bandwidth or delay—just hop numbers.


### RIP Version Comparison

| Feature | RIPv1 | RIPv2 |
|----------|--------|--------|
| Classful | Yes | No supports VLSM |
| Subnet Mask Info | Not included | Included in updates |
| Update Type | Broadcast | Multicast to 224.0.0.9 |
| Authentication | None | Supports text or MD5 |
| VLSM Support | No | Yes |

RIPv2 is widely used because it is more efficient and secure.


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

### When to Use RIP
Best for small networks with fewer than 15 routers.  
Benefits  
- Simple to configure  
- Low resource usage  
- Ideal for small branch networks  

Example A retail company with multiple stores uses RIP to connect routers across branches. The protocol automatically shares route info without complex setup.

For larger networks, OSPF is preferred due to RIP’s hop limit.

# Reference 
**Day 1** - [STP](https://claude.ai/public/artifacts/83161f5d-1c14-4ed0-8720-8f0c4d1c951b)  
**Day 2** - [Routing](https://claude.ai/public/artifacts/1921e117-1ea7-41d9-aefb-c5beb03b1c6b)  
**Day 3** - [RIP](https://claude.ai/public/artifacts/a28f54e1-e72b-4bdd-af38-6201ec24618a)

