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

# VLAN & Trunk – Quick Guide

## 🌐 VLAN (Virtual Local Area Network)
A **VLAN** is a *virtual* or **logical network** built inside a physical network.  
It lets you group devices together based on function (like HR or IT), even if those devices are plugged into **different switches**.

**Key points**
- Each VLAN behaves as its **own broadcast domain**, which helps:
  - cut down unnecessary network traffic
  - improve security between departments.
- Devices in different VLANs **cannot talk to each other** unless you configure **routing** (for example with a Layer-3 switch or router).

**Example setup**
- **VLAN 10** → HR team  
- **VLAN 20** → IT team  
- **VLAN 30** → Finance team  

Here, HR devices (VLAN 10) stay separate from IT (VLAN 20) until an L3 device is configured for inter-VLAN routing.

---

## 🔗 Trunk
A **trunk** is a single link (for example, a switch-to-switch cable) that can carry traffic for **many VLANs at the same time**.

**How it works**
- Uses **802.1Q tagging**: Each Ethernet frame gets a small tag to show which VLAN it belongs to.
- Allows VLAN traffic to pass **between switches**, so VLANs stay consistent across the network.

**Example**
The trunk link carries traffic for **both VLAN 10 and VLAN 20** across the two switches.

---

## ⚖️ VLAN vs Trunk

| Feature            | VLAN (Virtual Network)                         | Trunk (VLAN Carrier Link)                 |
|--------------------|--------------------------------------------------|--------------------------------------------|
| **Definition**     | Logical segmentation inside a physical network   | Link that transports traffic of many VLANs |
| **Scope**          | Works within a single switch or broadcast domain | Connects multiple switches or devices     |
| **Broadcast Domain** | Each VLAN is its own broadcast domain          | Can carry multiple VLANs across a link     |
| **Example**        | VLAN 10 = HR, VLAN 20 = IT                      | Trunk between Switch A and Switch B        |

---

### ✅ Quick Take
Think of **VLANs** as *separate rooms* inside a building, each with its own group of people.  
A **trunk** is like a *shared hallway* where people from every room can pass—while still wearing a badge (tag) that shows which room they belong to.

