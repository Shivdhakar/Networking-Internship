#  Lab: L3 Switch — Inter-VLAN Routing (Student Notes)

##  Objective
Configure **Inter-VLAN Routing** on a **Layer-3 Switch** so that hosts in different VLANs can communicate with each other.

## Devices Required
- 1 × **Layer-3 Switch** (e.g., Cisco 3560)  
- 1 × **Access Switch** *(optional)*  
- 2 × **PCs**  
- **Straight-through Ethernet Cables** (PC → Switch or Switch → Switch)  
  >  Crossover cable not required in Packet Tracer.

## Physical Topology (Simple)

# PC1 --- Fa0/1 (Access Switch) --- Gi0/1 (L3 Switch)
PC2 --- Fa0/2 (Access Switch) --- Gi0/2 (L3 Switch)

**OR (Direct Connection):**

PC1 --- Fa0/1 (L3 Switch)
PC2 --- Fa0/2 (L3 Switch)


---

##  Cabling
- **PC NIC → Switch Access Port:** Straight-through cable  
- **Access Switch → L3 Switch (Trunk):** Straight-through cable  
  *(Configure trunking on both ends)*

---

##  IP Addressing Table

| Device     | Interface   | VLAN | IP Address     | Subnet Mask       | Default Gateway |
|-------------|--------------|------|----------------|-------------------|-----------------|
| PC1         | NIC          | 10   | 192.168.10.10  | 255.255.255.0     | 192.168.10.1    |
| PC2         | NIC          | 20   | 192.168.20.10  | 255.255.255.0     | 192.168.20.1    |
| L3 Switch   | SVI VLAN 10  | 10   | 192.168.10.1   | 255.255.255.0     | -               |
| L3 Switch   | SVI VLAN 20  | 20   | 192.168.20.1   | 255.255.255.0     | -               |

---

##  Step-by-Step Configuration

###  Step 1: Physically Connect Devices
1. Connect **PC1** to **Switch port Fa0/1**.  
2. Connect **PC2** to **Switch port Fa0/2**.  
3. If using a separate access switch, connect it to the **L3 Switch trunk port (Gi0/1)**.  
   - If using **only the L3 switch**, connect both PCs directly to the L3 switch access ports.

---

###  Step 2: Create VLANs on L3 Switch
```bash
enable
configure terminal
vlan 10
 name SALES
exit
vlan 20
 name MARKETING
exit

# Configure Trunk (if Access Switch Used)

interface gig0/1
 switchport trunk encapsulation dot1q   ! (if supported)
 switchport mode trunk
exit

interface gig0/1
 switchport trunk encapsulation dot1q   ! (if supported)
 switchport mode trunk
exit

# Step 6: Create SVIs (Switch Virtual Interfaces)


