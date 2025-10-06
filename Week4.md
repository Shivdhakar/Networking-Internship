# Routing and its Types

## What is Routing?
Routing is the process of finding the **best path** for data packets to travel from **source to destination** in a network.

## Routing Types

### 1. Static Routing
- Routes are **manually added** by the network administrator.  
- Does **not update automatically** if the network changes.  
- **Simple, secure,** but less flexible.  
- Best suited for **small or stable** networks.

** Use When:**
- Small office or home networks.  
- Networks with few routers or routes.  
- When **stability and security** matter more than flexibility.

### 2. Dynamic Routing
- Routes are **automatically learned and updated** using routing protocols.  
- Adapts to **network changes** like link failure or new paths.  
- Best for **large and complex** networks.

** Use When:**
- Large organizations or **enterprise networks**.  
- **ISPs** (Internet Service Providers).  
- **Data centers** with frequently changing routes.

##  Troubleshooting Steps

### Static Routing
- Check if route details (IP, subnet mask, next-hop) are correct.  
- Test connectivity using **ping** or **traceroute**.  
- Make sure the **interface is up**.  
- View the routing table with `show ip route`.

###  Dynamic Routing
- Confirm the routing protocol is **enabled on correct interfaces**.  
- Check **neighbor relationships** (`show ip ospf neighbor`, `show ip eigrp neighbors`).  
- Look for wrong configurations (e.g., wrong area in OSPF, wrong AS in EIGRP).  
- Check for **unstable links or flapping networks**.  
- Use `debug ip routing` carefully to monitor route updates.

## Interdomain & Intradomain Routing

| Type | Description | Examples |
|------|--------------|-----------|
| **Intradomain Routing** | Used **within a single organization or AS**. Focus on internal routing efficiency. | RIP, OSPF, EIGRP |
| **Interdomain Routing** | Used **between different organizations or ASes**. Handles Internet-level routing. | BGP (Border Gateway Protocol) |


##  RIP (Routing Information Protocol)

- **Type:** Distance Vector Routing Protocol  
- **Metric Used:** Hop Count (maximum 15 hops)  
- **Updates:** Sent every 30 seconds  
- **Algorithm:** Bellman-Ford  
- **Versions:**  
  - RIP v1 → Classful (no subnet info)  
  - RIP v2 → Classless (supports subnet masks)  
- **Limitation:** Not suitable for large networks due to hop count limit.

##  Troubleshooting RIP
- Verify **network connectivity** (ping, tracert).  
- Check **RIP configuration** and network statements.  
- Ensure there are **no routing loops**.  
- Use commands like `show ip route` or `debug ip rip` to check routes.

---

## Example Scenarios
- **Intradomain:** A company uses **RIP or OSPF** to route data within its LAN.  
- **Interdomain:** The same company connects to an **ISP using BGP**.

