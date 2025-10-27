#  **Lab: L3 Switch — Inter-VLAN Routing **


##  **Objective**
Configure **Inter-VLAN Routing** on a **Layer-3 Switch** so that hosts in different VLANs can communicate with each other.



##  **Devices Required**
- **1 × Layer-3 Switch** (e.g., Cisco 3560)  
- **1 × Access Switch** *(optional)*  
- **2 × PCs**  
- **Straight-through Ethernet Cables** (PC → Switch or Switch → Switch)  
  >  *Crossover cable not required in Packet Tracer.*


##  **Physical Topology (Simple)**

PC1 --- Fa0/1 (Access Switch) --- Gi0/1 (L3 Switch)
PC2 --- Fa0/2 (Access Switch) --- Gi0/2 (L3 Switch)


**OR (Direct Connection):**
PC1 --- Fa0/1 (L3 Switch)
PC2 --- Fa0/2 (L3 Switch)



##  **Cabling**
- **PC NIC → Switch Access Port:** Straight-through cable  
- **Access Switch → L3 Switch (Trunk):** Straight-through cable  
  *(Configure trunking on both ends)*


## **IP Addressing Table**

| **Device** | **Interface** | **VLAN** | **IP Address** | **Subnet Mask** | **Default Gateway** |
|-------------|---------------|----------|----------------|-----------------|---------------------|
| PC1 | NIC | 10 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC2 | NIC | 20 | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |
| L3 Switch | SVI VLAN 10 | 10 | 192.168.10.1 | 255.255.255.0 | - |
| L3 Switch | SVI VLAN 20 | 20 | 192.168.20.1 | 255.255.255.0 | - |


##  **Step-by-Step Configuration**


###  **Step 1: Physically Connect Devices**
1. Connect **PC1** to **Switch port Fa0/1**.  
2. Connect **PC2** to **Switch port Fa0/2**.  
3. If using a separate access switch, connect it to the **L3 Switch trunk port (Gi0/1)**.  
   - If using **only the L3 switch**, connect both PCs directly to the L3 switch access ports.

### **Step 2: Create VLANs on L3 Switch**
```
enable
configure terminal
vlan 10
 name SALES
exit
vlan 20
 name MARKETING
exit
```
#Step 3: Assign Switch Ports to VLANs (Access Ports)

If PCs are connected directly to the L3 switch:

```interface range fa0/1
 switchport mode access
 switchport access vlan 10
exit

interface range fa0/2
 switchport mode access
 switchport access vlan 20
exit
 ```

 Step 4: Configure Trunk (if Access Switch Used)

On Access Switch (port toward L3 Switch):

```
interface gig0/1
 switchport trunk encapsulation dot1q   ! (if supported)
 switchport mode trunk
exit


On L3 Switch (port toward Access Switch):

interface gig0/1
 switchport trunk encapsulation dot1q   ! (if supported)
 switchport mode trunk
exit
```



 Step 5: Enable IP Routing on the L3 Switch
configure terminal
ip routing
exit

 Step 6: Create SVIs (Switch Virtual Interfaces)
```configure terminal
interface vlan 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit
```
interface vlan 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown
exit

 Step 7: Configure PCs (Manually)
```
PC1 Configuration

IP Address: 192.168.10.10
Subnet Mask: 255.255.255.0
Gateway: 192.168.10.1


PC2 Configuration

IP Address: 192.168.20.10
Subnet Mask: 255.255.255.0
Gateway: 192.168.20.1

```
 Step 8: Save Configuration
write memory

 Verification Commands
 On L3 Switch
show vlan brief           ! Verify VLANs exist and ports assigned
show ip interface brief   ! Check SVI interfaces and IPs
show ip route             ! See connected routes (192.168.10.0/24, 192.168.20.0/24)
show running-config       ! Confirm SVIs and 'ip routing' are configured

 On PCs

From PC1:
```
ping 192.168.10.1     ! Ping local gateway (should reply)
ping 192.168.20.10    ! Ping PC2 across VLANs (should reply if routing works)




