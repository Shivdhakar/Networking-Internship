# Routing and Its Types

## What is Routing?
Routing means finding the best path for data to travel from one device to another in a network.

## Types of Routing

### 1. Static Routing
- Routes are added **manually** by the admin.  
- Does **not change** if the network changes.  
- Easy and secure but not flexible.  
- Best for **small or fixed** networks.  

**Example:** 
Small office or home network.

### 2. Dynamic Routing
- Routers **learn routes automatically** using protocols.  
- **Updates routes** when network changes.  
- Best for **large or changing** networks.  

**Example:** 
ISP or enterprise network.

## Troubleshooting

**Static Routing**
- Check IP, subnet mask, and next-hop.  
- Use `ping` or `traceroute` to test.  
- Check if interface is up.  

**Dynamic Routing**
- Make sure routing protocol is on.  
- Check neighbors (`show ip ospf neighbor`).  
- Look for wrong area or AS number.  

##  Interdomain vs Intradomain 

| Type | Used For | Example |
|------|-----------|----------|
| **Intradomain** | Inside one organization | RIP, OSPF |
| **Interdomain** | Between different networks | BGP |

##  RIP (Routing Information Protocol)
- **Type:** Distance Vector  
- **Metric:** Hop count (max 15)  
- **Update:** Every 30 sec  
- **Algorithm:** Bellman-Ford  
- **Limit:** Not for big networks  

## Example
- Inside company → **RIP or OSPF**  
- Connect to ISP → **BGP**

