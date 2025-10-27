#  **Lab: DHCP Configuration on Layer-3 Switch**

##  **Objective**
Set up a **DHCP server** on a **Layer-3 Switch** to automatically assign IPs to devices in different VLANs.

##  **Devices Required**
- 1 × **Layer-3 Switch (e.g., Cisco 3560)**  
- 1 × **Access Switch** *(optional)*  
- 2 × **PCs**  
- **Straight-through Ethernet Cables**

##  **Network Topology**
PC1 --- Fa0/1 (L3 Switch)
PC2 --- Fa0/2 (L3 Switch)


## **IP Plan**

| VLAN | Network | Gateway | DHCP Range | Mask |
|------|----------|----------|-------------|-------|
| 10 (Sales) | 192.168.10.0 | 192.168.10.1 | 192.168.10.10–50 | /24 |
| 20 (Mktg)  | 192.168.20.0 | 192.168.20.1 | 192.168.20.10–50 | /24 |

##  **Configuration Steps**

###  **Create VLANs**
```bash
enable
conf t
vlan 10
 name SALES
vlan 20
 name MARKETING
exit
```
# Assign port
```
int fa0/1
 switchport mode access
 switchport access vlan 10
int fa0/2
 switchport mode access
 switchport access vlan 20
exit
```
# Enable ip routing & Configure VLAN Interfaces
```
conf t
ip routing
exit

int vlan 10
 ip address 192.168.10.1 255.255.255.0
 no shut
int vlan 20
 ip address 192.168.20.1 255.255.255.0
 no shut
exit
```
# Setup DHCP Pools
```
conf t

! VLAN 10
ip dhcp excluded-address 192.168.10.1 192.168.10.9
ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8

! VLAN 20
ip dhcp excluded-address 192.168.20.1 192.168.20.9
ip dhcp pool VLAN20
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 dns-server 8.8.8.8
exit


