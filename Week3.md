# Switches – L2 vs L3

## Switch in Simple Words
A switch is a box that joins many devices—like computers, printers, or servers—inside one network (for example, a company LAN).  
Instead of sending every data packet to all devices like a hub does, it delivers the data only to the exact device that needs it.  
This keeps the network fast and avoids unnecessary traffic.

---

## Layer 2 (L2) Switch
- Works at the **Data Link layer** in the OSI model.  
- Forwards data using the **MAC address** of each device.  
- Commonly used to connect computers inside the same LAN.

**Downside:**  
👉 Cannot pass data between two different networks; it only works inside one network.

---

## Layer 3 (L3) Switch
- Works at the **Network layer** of the OSI model.  
- Uses **IP addresses** to move data.  
- Can perform **routing** tasks (like a router) while still doing normal switch functions.  

**When to Use:**  
👉 Useful for bigger setups where you need both quick LAN switching and communication between multiple networks.

---

## Quick Comparison: L2 vs L3

| Feature        | L2 Switch | L3 Switch |
|-----------------|----------|----------|
| **Layer**       | Data Link (Layer 2) | Network (Layer 3) |
| **Address Type**| MAC address         | IP address       |
| **Main Job**    | Switch traffic inside one LAN | Switch + route between networks |
| **Performance** | Very fast and simple | Slightly slower, does more work |
| **Example**     | Small office LAN     | Large network with VLANs |

---
