# ACL Lab – Cisco Packet Tracer
## Objective

Configure and verify Access Control List (ACL) to control network traffic.

# Topology

1 Router (R1)

2 Switches (S1, S2)

4 PCs (PC1–PC4)

Cables: Copper Straight-Through

# Step 1: Setup & Cabling

Open Cisco Packet Tracer.

Drag 1 Router, 2 Switches, 4 PCs.

Connect:

PC1/PC2 → Switch1

PC3/PC4 → Switch2

Switch1 → Router G0/0

Switch2 → Router G0/1

# Step 2: Assign IPs
```
Device	IP Address	Subnet Mask	Gateway
PC1	192.168.10.10	255.255.255.0	192.168.10.1
PC2	192.168.10.11	255.255.255.0	192.168.10.1
PC3	192.168.20.10	255.255.255.0	192.168.20.1
PC4	192.168.20.11	255.255.255.0	192.168.20.1
```
Configure each PC: Desktop → IP Configuration

# Step 3: Router Configuration
```
enable
configure terminal

interface g0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit

interface g0/1
ip address 192.168.20.1 255.255.255.0
no shutdown
exit
```
do show ip interface brief

# Step 4: Test Connectivity
```
From PC1 → ping 192.168.20.10
```

# Step 5: Configure Standard ACL
```
enable
configure terminal
access-list 1 deny 192.168.10.10
access-list 1 permit any

interface g0/0
ip access-group 1 in
exit
```
# Step 6: Test ACL
```
PC1 → ping 192.168.20.10 →  Fail

PC2 → ping 192.168.20.10 →  Success
```

# Step 7: Verify & Save
```
show access-lists
copy running-config startup-config
```
# Result

PC1 blocked by ACL.

Other PCs allowed.

ACL works as expected.
