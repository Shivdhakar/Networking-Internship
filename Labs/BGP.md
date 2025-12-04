# Lab Objective

In this lab I will configure BGP (Border Gateway Protocol) between two different Autonomous Systems (AS).
BGP is used on the internet for sharing routes between service providers and large networks.


 ## Devices  I Used
 Routers

### 2 × Cisco 2901 routers (you can use 2811/1941 also)

 PCs

2 × Standard PCs

 Cables

#### Serial DCE cable for router-to-router

we use Copper Straight-Through cable for PC-to-router

## Device Connections
 Router R1 → Router R2 (Serial)

### we Use Serial DCE cable

R1 → Serial0/0/0

R2 → Serial0/0/0

 PC1 → R1

Use Copper Straight-Through

PC1 FastEthernet0 → R1 GigabitEthernet0/0

 PC2 → R2

Use Copper Straight-Through

PC2 FastEthernet0 → R2 GigabitEthernet0/0

## IP Addressing
 PC1
 ~~~
IP Address: 10.1.1.10
Subnet Mask: 255.255.255.0
Gateway: 10.1.1.1
~~~

 PC2
 ~~~
IP Address: 20.1.1.10
Subnet Mask: 255.255.255.0
Gateway: 20.1.1.1
~~~

## Router Configurations

 Router R1 Configuration
 ~~~
enable
configure terminal

interface g0/0
 ip address 10.1.1.1 255.255.255.0
 no shutdown

interface s0/0/0
 ip address 11.0.0.1 255.255.255.252
 clock rate 64000
 no shutdown

router bgp 65001
 neighbor 11.0.0.2 remote-as 65002
 network 10.1.1.0 mask 255.255.255.0

end
write
~~~

Router R2 Configuration
~~~
enable
configure terminal

interface g0/0
 ip address 20.1.1.1 255.255.255.0
 no shutdown

interface s0/0/0
 ip address 11.0.0.2 255.255.255.252
 no shutdown

router bgp 65002
 neighbor 11.0.0.1 remote-as 65001
 network 20.1.1.0 mask 255.255.255.0

end
write
~~~

## Verification Commands

for Check BGP Neighbor
~~~
show ip bgp summary
~~~

Expected:
~~~
State = Established
~~~

### Check BGP Routing Table
~~~
show ip bgp
~~~

### Check Router’s IP Routes
~~~
show ip route
~~~

### End-to-End Ping (PC1 → PC2)

On PC1: we use
~~~ 
ping 20.1.1.10
~~~

Ping should be successful.
