# OSPF (Open Shortest Path First)

## What is OSPF?
OSPF is a dynamic routing protocol that finds the best path for data in a network.  
It works inside a single Autonomous System (AS) and uses the Link State Routing algorithm.

## Key Concepts
- **Link-State Protocol:** Routers share info about their direct links.  
- **Area:** Network is divided into areas to improve performance.  
- **Router ID:** Unique ID of a router (highest IP or manually set).  
- **LSA (Link-State Advertisement):** Used to share link information.  
- **Cost:** Metric based on bandwidth to choose the best route.  
- **DR/BDR:** Designated and Backup Routers reduce network traffic.

## How OSPF Works
1. Routers send Hello packets to find neighbors.  
2. They exchange LSAs to learn the network.  
3. Each router builds a Link-State Database (LSDB).  
4. Dijkstra’s algorithm calculates the shortest path.  
5. Routing table is updated with best routes.

## OSPF Areas
- **Area 0:** Backbone area, main part of the network.  
- **Stub Area:** No external routes allowed.  
- **NSSA:** Allows limited external routes.

## Example
Used in big networks like enterprises or ISPs for fast and loop-free routing.

## Troubleshooting
- Check neighbors → `show ip ospf neighbor`  
- Verify interface and area ID  
- Check router ID  
- Match hello/dead timers  
- View learned routes → `show ip route ospf`

  #  EIGRP (Enhanced Interior Gateway Routing Protocol)

##  Basic Info
- Full Form: Enhanced Interior Gateway Routing Protocol  
- Type: Dynamic Routing Protocol  
- Developed by: Cisco  
- Category: Hybrid (Distance Vector + Link State)

##  Working
- Uses **DUAL (Diffusing Update Algorithm)** for best path  
- Metric: Bandwidth + Delay + Load + Reliability  
- Sends **partial & triggered updates** (not full)

## Values
- Administrative Distance: 90 (internal), 170 (external)  
- Protocol Number: 88  

##  Features
- Classless (supports VLSM & CIDR)  
- Supports IPv4 and IPv6  
- Forms neighbor relationships  


