# Router Redundancy and Firewall

In a corporate network, the main goals are:

- The network should not go down if one device fails.  
- Data should be safe and private when it travels over the internet.  
- Only authorized users should be able to access company resources.

To achieve this, companies use:

- Router redundancy  
- Firewalls  
- VPN (Virtual Private Network)  
- SSL / TLS (for secure communication)

<br/>

# Router Redundancy

## Why Do We Need Router Redundancy?

Every computer in a network uses a default gateway (usually a router) to reach:

- The internet  
- Other networks  
- Cloud services  

If the only router in the network goes down:

❌ No internet  
❌ No communication  
❌ Network failure  

This situation is called **Single Point of Failure**.

To avoid this problem, companies add another router as a backup.  
If one router fails, the second automatically takes over.

This setup is called **Router Redundancy**.

<br/>

## What Is the Basic Idea of Router Redundancy?

Imagine two teachers sharing one classroom:

- **Teacher A** teaches.  
- **Teacher B** waits outside in case Teacher A gets sick.

Same in networking:

- Two routers share one **virtual IP address** (example: `192.168.1.1`).  
- PCs use this virtual IP as their default gateway.

### Roles in Router Redundancy

- **Active Router / Master** → currently forwarding traffic  
- **Standby Router / Backup** → waiting to take over  

If the active router fails:

- The standby router becomes the new active gateway instantly  
- Users do **not** notice any change  

This automatic switching is handled by **FHRP protocols**.

<br/>

# First Hop Redundancy Protocols (FHRP)

These protocols help two or more routers act as **one single gateway**.

We study 3 main types:

1. **HSRP** (Cisco only)  
2. **VRRP** (Open standard)  
3. **GLBP** (Cisco only + load balancing)

<br/>

## First Hop Redundancy Protocols (FHRP)

These protocols help two or more routers act as one single gateway.

We study 3 main types:

HSRP (Cisco only)

VRRP (Open standard)

GLBP (Cisco only + load balancing)


<br/>

## 1. HSRP (Hot Standby Router Protocol)
  
HSRP is a Cisco protocol that provides router redundancy by allowing two or more routers to work together and act like a single gateway for the network.

In simple words

- Two routers share the same gateway IP.  
- One router is *Active* and the other waits as *Backup*.  
- If the Active router fails the Backup router automatically takes over.

<br/>

###  How HSRP Works
- Two routers form an HSRP group.  
- They create a **virtual IP address** (example: `192.168.1.1`).  
- All PCs use this virtual IP as their default gateway.  
- The router with the highest priority becomes **Active**.  
- The second router becomes **Standby**.  
- Routers send *hello messages* to check if the Active router is alive.  
- If the Active router fails → the Standby router becomes the new Active router *without interruption*.

<br/>

###  Why HSRP Is Used?
- To avoid network downtime  
- To remove single point of failure  
- For Cisco-only environments  


<br/>

## 2. VRRP (Virtual Router Redundancy Protocol)


VRRP is an open-standard redundancy protocol that allows multiple routers to share a virtual IP address and provide a backup gateway for hosts.

In simple words

- VRRP works like HSRP but can run on routers from different vendors (Cisco, Juniper, HP).  
- One router is the **Master**, and others are **Backup**.
- 
<br/>

###  How VRRP Works
- Routers share one virtual IP.  
- The router with the highest priority becomes **Master**.  
- All other routers act as Backup routers.  
- If the Master fails → a Backup becomes the new Master automatically.  
- Works across multiple vendors (multi-vendor support).

<br/>

###  Why VRRP Is Used?
- For networks with mixed devices  
- Redundancy across different brands  
- Faster failover compared to HSRP  

<br/>

## 3. GLBP (Gateway Load Balancing Protocol)

GLBP is a Cisco protocol that provides both router redundancy and load balancing by allowing multiple routers to actively forward traffic at the same time.

In simple words

- GLBP is different from HSRP and VRRP.  
- Instead of one router working and others waiting, **all routers can share the traffic**.

<br/>

###  How GLBP Works

- Routers form a GLBP group.  
- They use one **virtual IP**, like HSRP and VRRP.  
- GLBP assigns **multiple virtual MAC addresses**.  
- Each host gets a different virtual MAC address.  
- Traffic is distributed across all routers.  
- If one router fails → remaining routers continue forwarding traffic.

<br/>

###  Why GLBP Is Used?
- Provides load balancing across multiple routers  
- Provides redundancy at the same time  
- All routers are used efficiently (no idle router)

<br/>

##  Comparison  Table

| Feature        | HSRP        | VRRP           | GLBP                         |
|----------------|-------------|----------------|-------------------------------|
| Standard       | Cisco-only  | Open standard  | Cisco-only                    |
| Purpose        | Redundancy only | Redundancy only | Redundancy + Load Balancing |
| Active Routers | 1 Active    | 1 Master       | Multiple Active              |
| Backup Routers | Standby     | Backup routers | Secondary routers support    |
| Failover       | Yes         | Yes (faster)   | Yes                           |
| Virtual IP     | ✔           | ✔              | ✔                             |
| Virtual MAC    | 1           | 1              | Multiple                      |

<br/>

##  Simple One-Line Definition

**HSRP:** Cisco protocol where one router is Active and another is Standby, providing gateway redundancy.

**VRRP:** Open-standard redundancy protocol similar to HSRP, but supports multi-vendor routers.

**GLBP:** Cisco protocol that provides redundancy and load balancing by allowing multiple routers to forward traffic together.


## Example of Router Redundancy
A company uses two routers to avoid network failure:

- Router 1 = Active Router  
- Router 2 = Standby Router
- Both share the same virtual gateway IP `192.168.1.1`.
- 
If Router 1 fails due to power issues, Router 2 immediately becomes active.  
Users continue accessing the network without any interruption.  
This is achieved through protocols like **HSRP**, **VRRP**, or **GLBP**.
---

<br/>

# Firewalls in Corporate Networks

## What Is a Firewall?

A firewall is a security device or software program that protects a computer network by monitoring and controlling all the data that enters or leaves it. It sits between the internal network (such as a company’s LAN) and the outside world (such as the internet). The firewall analyzes each packet of data and decides whether to allow or block it based on rules defined by the organization. Its main purpose is to prevent unauthorized access, stop harmful traffic, and ensure that only safe and approved communication is permitted. Without a firewall, a network becomes vulnerable to hackers, malware, and unwanted external connections.

A good example to understand it:

**A firewall works like a security guard at the main gate of a company.**

It checks:

- Who is coming in?  
- Who is going out?  
- Are they allowed to enter or leave?  
- Are they safe?  

If traffic follows the rules → it is allowed.  
If not → it is blocked.

<br/>

## Why Do Companies Use Firewalls?

Companies use firewalls to keep their network safe. They help in:

1. **Blocking unauthorized access**  
   Hackers or unknown users should not enter the internal network.

2. **Allowing only required services**  
   Example: Only allow HTTP, HTTPS, SSH, and block dangerous ports.

3. **Protecting against attacks**  
   Firewalls stop malware, port scans, brute-force attempts, etc.

4. **Creating different security zones**  
   - **Internal LAN** → For employees  
   - **DMZ (Demilitarized Zone)** → For public servers like web or mail server  
   - **Internet** → Untrusted zone  

This separation makes the network more secure.

<br/>

# Types of Firewalls

Firewalls can be of different types based on how they inspect and filter network traffic.  
Below are the main types explained in an easy and detailed way.

## 1. Packet-Filtering Firewall

A packet-filtering firewall is the simplest and oldest type of firewall. It checks each packet of data based on basic information such as

- Source IP address  
- Destination IP address  
- Port number  
- Protocol (TCP/UDP)

It works using **simple ACL (Access Control List)** rules.

**Layers:** Network & Transport layers (Layer 3 & 4)

**Example:**  
Allow traffic from 192.168.1.0/24 to port 80 (HTTP).

<br/>

## 2. Stateful Firewall

A stateful firewall is smarter than packet-filtering.It **remembers the state of the connection**.  
It knows:

- Which connections are new  
- Which connections are already established  
- Which connections are related to another connection  

This makes it **much more secure**.

Example:  
If we open a website, the firewall allows the return traffic because it knows the connection is yours.

<br/>

## 3. Application Layer Firewall /[ Next-Generation Firewall (NGFW) ]

An application layer firewall, also called a Next-Generation Firewall (NGFW), is the most advanced type. It can look deep inside the traffic and identify which application is being used such as

- Facebook  
- YouTube  
- WhatsApp  
- Gmail  

It can filter traffic by:

- Application name  
- User identity  
- URL categories  
- Content type  

It also provides advanced security features:

- IDS/IPS (Intrusion Detection / Prevention System)  
- Deep Packet Inspection  
- Antivirus / Malware filtering  
- URL filtering  

This is commonly used in modern companies.

<br/>

## 4. Host-Based Firewall

A firewall that runs on individual devices such as:

- Windows Defender Firewall  
- macOS Firewall  
- Linux iptables / ufw  

It protects that single machine only.

<br/>

# Simple Firewall Rule Example

A small company firewall may have rules like:

1. **Allow outgoing HTTP/HTTPS** from LAN to Internet  
   (Employees can browse websites)

2. **Allow incoming HTTPS** only to the web server in DMZ  
   (Customers can visit the company website)

3. **Block Telnet (port 23)** everywhere  
   (Because Telnet is unsafe and unencrypted)

4. **Deny all other traffic by default**  
   (Only allow what is required; block everything else)

<br/>

## What This Achieves

- Employees can safely access the internet.  
- Customers can open the company website.  
- Dangerous and outdated services are blocked.  
- The internal network stays secure and protected.

---



