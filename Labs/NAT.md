 # Static NAT Lab – Cisco Packet Tracer

 ## Objective

Configure Static NAT on a router to allow an inside local address to be mapped to an inside global address for Internet access.

# Topology

1 Router (R1)

1 Switch (S1)

2 PCs (PC1 - inside, PC2 - outside)

# Step 1: Setup & Cabling

Open Cisco Packet Tracer.

Drag and drop:

1 Router, 1 Switch, 2 PCs

## Connect devices:

PC1 → Switch → Router (G0/0)

PC2 → Router (G0/1) using a straight-through cable

# Step 2: Assign IP Addresses
Device	Interface	IP Address	Subnet Mask	Gateway
```
PC1 (Inside)	Fa0	192.168.10.10	255.255.255.0	192.168.10.1
PC2 (Outside)	Fa0	200.0.0.2	255.255.255.0	200.0.0.1
```
Configure via: Desktop → IP Configuration

# Step 3: Router Interface Configuration

```
enable
configure terminal

# Inside Interface
interface gigabitEthernet 0/0
ip address 192.168.10.1 255.255.255.0
ip nat inside
no shutdown
exit

# Outside Interface
interface gigabitEthernet 0/1
ip address 200.0.0.1 255.255.255.0
ip nat outside
no shutdown
exit
```
 Step 4: Configure Static NAT
```
Map the inside local (private) IP to a public (global) IP.

ip nat inside source static 192.168.10.10 200.0.0.10
```

 # Step 5: Verify NAT Configuration
 ```
show ip nat translations
```

# Output Example:

```
Pro  Inside local      Inside global     Outside local     Outside global
---  192.168.10.10     200.0.0.10        ---                ---
```

# Step 6: Test Connectivity
```
On PC2 (Outside Network), ping 200.0.0.10
```
 ## The ping should succeed, meaning NAT translation is working.

# Step 7: Save Configuration
```
copy running-config startup-config
```
 ## Result

Static NAT configured successfully.

Private IP (192.168.10.10) translated to Public IP (200.0.0.10).

Communication between inside and outside networks established.
