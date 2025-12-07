#  Networking Troubleshooting Commands & Uses

<br/>

##  Networking Basics


<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `ping <IP>` | Check connectivity | Tests if a device is reachable and measures response time. |
| `tracert <IP>` (Windows) / `traceroute <IP>` (Linux) | Trace route | Shows the path packets take to reach a destination. |
| `ipconfig` / `ifconfig` | Check IP configuration | Displays IP address, subnet mask, and gateway details. |
| `arp -a` | View ARP table | Lists MAC and IP address mapping in the network. |
| `netstat` | View network connections | Shows active connections and listening ports. |



<br/>

##  Types of Networking (LAN, WAN, MAN)

<br/>




| Type | Use | Description |
|------|-----|-------------|
| LAN | Local communication | Connects computers in a small area (office, home). |
| WAN | Long-distance networking | Connects LANs over large distances (like the Internet). |
| MAN | Metropolitan area | Covers a city or large campus area. |
| WLAN | Wireless LAN | Uses Wi-Fi to connect devices within a limited range. |





<br/>

##  OSI Model

<br/>



| Layer | Function | Example/Tool |
|--------|-----------|---------------|
| Physical | Cable & signal transmission | Ethernet cables, hubs |
| Data Link | Frame transfer & MAC address | Switch, ARP |
| Network | IP routing | Router, IP address |
| Transport | Reliable data delivery | TCP/UDP |
| Session | Connection setup | Remote login |
| Presentation | Data format conversion | Encryption, compression |
| Application | User interaction | Browser, email client |




<br/>

## TCP/IP Model

<br/>

| Layer | Function | Protocols/Commands |
|--------|-----------|--------------------|
| Network Access | Physical data delivery | Ethernet, ARP |
| Internet | Logical addressing | IP, ICMP |
| Transport | End-to-end communication | TCP, UDP |
| Application | User services | HTTP, FTP, DNS, SMTP |

<br/>

## L2 & L3 Concepts (VLANs and Trunks)

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `vlan <ID>` | Create VLAN | Segments the switch into logical groups. |
| `switchport access vlan <ID>` | Assign port to VLAN | Connects port to a specific VLAN. |
| `switchport mode trunk` | Configure trunk port | Allows multiple VLANs over one link. |
| `show vlan brief` | Verify VLANs | Displays all VLANs and their assigned ports. |
| `show interfaces trunk` | Verify trunks | Checks trunk status and allowed VLANs. |

<br/>

## Spanning Tree Protocol (STP)

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `show spanning-tree` | Check STP status | Shows root bridge, ports, and topology. |
| `spanning-tree vlan <ID> priority <value>` | Set root bridge | Forces a switch to be root by lowering priority. |
| `spanning-tree portfast` | Enable fast access port | Bypasses STP delay on access ports. |

<br/>

## Routing (General)

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `show ip route` | View routing table | Displays all learned and static routes. |
| `ip route <network> <mask> <next-hop>` | Add static route | Manually defines a path to a destination network. |
| `show ip interface brief` | Check interface status | Lists interfaces, IPs, and their state. |


<br/>

## RIP (Routing Information Protocol)

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `router rip` | Enable RIP | Starts the RIP process. |
| `network <network>` | Advertise network | Includes a network in RIP updates. |
| `show ip protocols` | Verify RIP info | Displays routing protocol details. |
| `show ip route rip` | View RIP routes | Shows routes learned through RIP. |

<br/>

## OSPF (Open Shortest Path First)

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `router ospf <process-id>` | Start OSPF | Enables OSPF routing. |
| `network <network> <wildcard> area <area>` | Add network | Assigns networks to OSPF areas. |
| `show ip ospf neighbor` | View neighbors | Checks OSPF adjacency status. |
| `show ip ospf interface` | Interface info | Displays OSPF details per interface. |

<br/>

## EIGRP (Enhanced Interior Gateway Routing Protocol)

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `router eigrp <ASN>` | Start EIGRP | Enables EIGRP routing. |
| `network <network>` | Advertise network | Adds network to EIGRP updates. |
| `show ip eigrp neighbors` | Verify neighbors | Displays connected EIGRP neighbors. |
| `show ip eigrp topology` | View topology | Shows all learned routes and successors. |
<br/>

## BGP (Border Gateway Protocol)

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `router bgp <ASN>` | Start BGP | Enables BGP process. |
| `neighbor <IP> remote-as <ASN>` | Configure peer | Sets up BGP neighbor connection. |
| `network <network> mask <mask>` | Advertise route | Shares a network in BGP. |
| `show ip bgp summary` | Verify neighbors | Displays BGP session and status. |

<br/>

## DHCP (Dynamic Host Configuration Protocol)

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `ip dhcp pool <name>` | Create DHCP pool | Defines a DHCP address pool. |
| `network <network> <mask>` | Define range | Specifies address range for clients. |
| `default-router <IP>` | Set gateway | Sets default gateway for clients. |
| `show ip dhcp binding` | Verify leases | Lists IPs assigned by DHCP. |

<br/>

## NAT & PAT

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `ip nat inside source static <in> <out>` | Static NAT | Maps one private IP to one public IP. |
| `ip nat inside source list <ACL> interface <int> overload` | PAT | Allows many private IPs to share one public IP. |
| `show ip nat translations` | Check NAT table | Displays active NAT/PAT translations. |

<br/>

## ACL (Access Control List)

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `access-list <no> permit/deny <protocol> <source> <dest>` | Create ACL | Defines traffic filtering rules. |
| `ip access-group <no> in/out` | Apply ACL | Attaches ACL to an interface. |
| `show access-lists` | Verify ACLs | Shows configured ACL rules. |

<br/>

## LAN Switching

<br/>

| Command | Use | Description |
|----------|-----|-------------|
| `show mac address-table` | View MAC table | Lists MAC addresses learned on switch ports. |
| `clear mac address-table dynamic` | Clear table | Removes learned MAC addresses. |
| `switchport mode access/trunk` | Set port type | Defines access or trunk mode. |
| `show interfaces status` | Interface overview | Displays port speed, duplex, and VLAN info. |

<br/>

## Network Troubleshooting Commands

<br/>

| Command | Use | Description |
|--------|------|------------|
| `ping <ip>` | Test connectivity | Sends ICMP Echo packets to verify device reachability |
| `traceroute <ip>` / `tracert <ip>` | Trace network path | Shows the route packets take hop-by-hop to reach the destination |
| `telnet <ip> <port>` | Test port access | Checks if a specific service/port on a remote device is reachable |
| `ssh user@ip` | Secure remote login | Allows secure access to remote devices for configuration and management |

<br/>

###  VPN Commands
| Command | Use | Description |
|---------|-----|-------------|
| `show crypto isakmp sa` | VPN status | Displays active IKE security associations |
| `show crypto ipsec sa` | IPsec tunnels | Shows established IPsec tunnels & traffic stats |
| `clear crypto isakmp` | Reset VPN | Clears IKE negotiations |
| `show vpn-sessiondb` | Session info | Lists active VPN users/sessions |

<br/>

###  Firewall & Security
| Command | Use | Description |
|---------|-----|-------------|
| `show access-lists` | View ACLs | Displays configured access control lists |
| `show ip nat translations` | NAT status | Shows active NAT translations |
| `show firewall` | Firewall rules | Displays active firewall policies |
| `debug ip packet` | Packet trace | Debugs packet flow (use cautiously) |


<br/>


###  Tuning & Performance
| Command | Use | Description |
|---------|-----|-------------|
| `show processes cpu` | CPU usage | Monitors router/switch CPU utilization |
| `show memory` | Memory stats | Displays memory usage & availability |
| `show logging` | Log analysis | Reviews system event logs |
| `terminal monitor` | Live logging | Enables real-time log display |


<br/>

###  Router Redundancy (HSRP/GLBP/VRRP)
| Command | Use | Description |
|---------|-----|-------------|
| `show standby` | HSRP status | Displays Hot Standby Router Protocol status |
| `show glbp` | GLBP status | Gateway Load Balancing Protocol status |
| `show vrrp` | VRRP status | Virtual Router Redundancy Protocol status |
| `standby preempt` | Priority takeover | Enables preemptive failover |

---

