# OSPF Lab – Cisco Packet Tracer

 ## Objective

Configure OSPF (Open Shortest Path First) on routers to enable dynamic routing between networks.

# Topology

3 Routers (R1, R2, R3)

3 Switches (S1, S2, S3)

3 PCs (PC1, PC2, PC3)

Connections:

R1 ↔ R2 ↔ R3 (Serial Links)

PCs connected via switches to each router

# Step 1: Setup & Cabling

Open Cisco Packet Tracer.

Drag 3 Routers, 3 Switches, and 3 PCs.

Connect devices using Copper Straight-Through (for LAN) and Serial DCE cables (for WAN links).

Example connections:

PC1 → Switch1 → R1 (G0/0)

PC2 → Switch2 → R2 (G0/0)

PC3 → Switch3 → R3 (G0/0)

R1 → R2 (S0/0/0)

R2 → R3 (S0/0/1)

# Step 2: Assign IP Addresses
```
Device	Interface	IP Address	Subnet Mask	Gateway
PC1	Fa0	192.168.1.10	255.255.255.0	192.168.1.1
PC2	Fa0	192.168.2.10	255.255.255.0	192.168.2.1
PC3	Fa0	192.168.3.10	255.255.255.0	192.168.3.1
```

# Step 3: Router IP Configuration
```
R1
enable
configure terminal
interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface s0/0/0
ip address 10.0.0.1 255.255.255.252
no shutdown
exit

R2
enable
configure terminal
interface g0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

interface s0/0/0
ip address 10.0.0.2 255.255.255.252
no shutdown
exit

interface s0/0/1
ip address 10.0.0.5 255.255.255.252
no shutdown
exit

R3
enable
configure terminal
interface g0/0
ip address 192.168.3.1 255.255.255.0
no shutdown
exit

interface s0/0/1
ip address 10.0.0.6 255.255.255.252
no shutdown
exit
```
# Step 4: Configure OSPF on All Routers
```
R1
router ospf 1
network 192.168.1.0 0.0.0.255 area 0
network 10.0.0.0 0.0.0.3 area 0
exit

R2
router ospf 1
network 192.168.2.0 0.0.0.255 area 0
network 10.0.0.0 0.0.0.3 area 0
network 10.0.0.4 0.0.0.3 area 0
exit

R3
router ospf 1
network 192.168.3.0 0.0.0.255 area 0
network 10.0.0.4 0.0.0.3 area 0
exit
```

 Step 5: Verify OSPF Neighbors
 ```
show ip ospf neighbor
```

 We see R1 ↔ R2 and R2 ↔ R3 as neighbors.

# Step 6: Verify Routing Table
```
show ip route ospf
```

# Each router should now have routes to all three networks (192.168.1.0, 192.168.2.0, 192.168.3.0).

🧾 Step 7: Test Connectivity
```
From PC1, ping:

ping 192.168.2.10
ping 192.168.3.10
```

# If replies received, OSPF is working.
