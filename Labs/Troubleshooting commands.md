# Ping • Traceroute • Telnet • SSH

## Lab Objective

In this lab we will learn and practice the four basic troubleshooting commands used by every network engineer so i used all four troubleshooting commands in one lab.

Ping – To check connectivity

Traceroute / Tracert – To check the path packets take

Telnet – To test remote device port access

SSH – To securely log in to another device

##  Devices Required
 Routers

### 2 × Cisco Routers (2911 / 1941 / 2811) we can use any of these 

 PCs / Servers

PC1 (source)

PC2 (destination server)

 Cables

### Copper Straight-Through (PC ↔ Router)

Serial DCE (Router ↔ Router)

##  Device Connections we use
 Router R1 ↔ Router R2

Use Serial DCE

### R1 Serial0/0/0 ↔ R2 Serial0/0/0

 PC1 ↔ R1

### PC1 FastEthernet0 ↔ R1 GigabitEthernet0/0

 PC2 ↔ R2

### PC2 FastEthernet0 ↔ R2 GigabitEthernet0/0

## IP Addressing

 PC1
 ~~~
IP: 10.0.0.10
Mask: 255.255.255.0
Gateway: 10.0.0.1
~~~
 PC2
 ~~~
IP: 20.0.0.10
Mask: 255.255.255.0
Gateway: 20.0.0.1
~~~

## Router Configurations

 ### R1 Router
 ~~~
enable
configure terminal

interface g0/0
 ip address 10.0.0.1 255.255.255.0
 no shutdown

interface s0/0/0
 ip address 11.0.0.1 255.255.255.252
 clock rate 64000
 no shutdown

router rip
 version 2
 network 10.0.0.0
 network 11.0.0.0

end
write
~~~

### R2 Router
~~~
enable
configure terminal

interface g0/0
 ip address 20.0.0.1 255.255.255.0
 no shutdown

interface s0/0/0
 ip address 11.0.0.2 255.255.255.252
 no shutdown

router rip
 version 2
 network 20.0.0.0
 network 11.0.0.0

end
write
~~~
## Now we Configure Telnet & SSH on R2 (Destination)
 Set hostname & domain
 ~~~
hostname R2
ip domain-name lab.com
~~~
 Create username & password
 ~~~
username admin privilege 15 secret admin123
~~~
 Enable SSH
 ~~~
crypto key generate rsa
~~~



### Enable VTY lines
~~~
line vty 0 4
 login local
 transport input telnet ssh
~~~

 Set enable password
 ~~~
enable secret cisco
~~~

## LAB TESTS of all four commands 

Now PC1 will run all four troubleshooting commands.

### Test 1: Ping
 Purpose:

To check if PC2 (20.0.0.10) is reachable.

### Command (run on PC1):
~~~
ping 20.0.0.10
~~~
#### Expected Result:

Replies like:
~~~
Reply from 20.0.0.10: bytes=32 time<1ms TTL=64
~~~

If ping fails → there is a connectivity problem.

## Test 2: Traceroute / Tracert
 Purpose:

To check the path packet takes from PC1 to PC2.

 Command on PC1:
 ~~~
tracert 20.0.0.10
~~~
 Expected Result:

we  will see hops:
~~~
1   10.0.0.1   (R1)
2   11.0.0.2   (R2)
3   20.0.0.10  (PC2)
~~~

If traceroute stops at a hop  issue is at that router.

 ## Test 3: Telnet 
 Purpose:

To check if R2 telnet port is open.

 Command (PC1):
 ~~~
telnet 20.0.0.1
~~~

 Expected Output:
 ~~~
Password required
~~~

If you  we get connection refused / timeout  Telnet port is blocked.

## Test 4: SSH (Secure login test)
 Purpose:

SSH is a secure way to log in to devices.

 Command (PC1):
 ~~~
ssh -l admin 20.0.0.1
~~~
 Expected:
 ~~~
Password:
~~~

After entering password we you will enter R2.

SSH is safer than Telnet because it uses encryption.








