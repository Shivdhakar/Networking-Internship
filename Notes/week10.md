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

##  Router Redundancy

### Why do we need Router Redundancy?

Every computer in a network uses a default gateway (usually a router) to reach:

The internet

Other networks

Cloud services

If the only router in the network goes down:

❌ No internet
❌ No communication
❌ Network failure

#### This situation is called: { Single point of failure }

To avoid this problem, companies add another router as a backup.
If one router fails, the second one automatically takes over.

#### This setup is called: { Router Redundancy }

## What is the basic idea of Router Redundancy?

Imagine two teachers sharing one classroom:

Teacher A teaches.

Teacher B waits outside in case Teacher A gets sick.

Same in networking:

Two routers share one virtual IP address (example: 192.168.1.1), and PCs use this one virtual IP as the gateway.

Roles:

Active Router / Master → currently forwarding traffic

Standby Router / Backup → waiting to take over

If the active router dies:

<> The standby router becomes the new active gateway instantly
<> Users do not notice the change

#### This automatic switching is done by FHRP protocols:

HSRP

VRRP

GLBP

## First Hop Redundancy Protocols (FHRP)

These protocols help two or more routers act as one single gateway.

We study 3 main types:

HSRP (Cisco only)

VRRP (Open standard)

GLBP (Cisco only + load balancing)



## 1. HSRP (Hot Standby Router Protocol)
  
HSRP is a Cisco protocol that provides router redundancy by allowing two or more routers to work together and act like a single gateway for the network.

In simple words

- Two routers share the same gateway IP.  
- One router is *Active* and the other waits as *Backup*.  
- If the Active router fails the Backup router automatically takes over.

---

###  How HSRP Works
- Two routers form an HSRP group.  
- They create a **virtual IP address** (example: `192.168.1.1`).  
- All PCs use this virtual IP as their default gateway.  
- The router with the highest priority becomes **Active**.  
- The second router becomes **Standby**.  
- Routers send *hello messages* to check if the Active router is alive.  
- If the Active router fails → the Standby router becomes the new Active router *without interruption*.

---

###  Why HSRP Is Used?
- To avoid network downtime  
- To remove single point of failure  
- For Cisco-only environments  

---

## 2. VRRP (Virtual Router Redundancy Protocol)


VRRP is an open-standard redundancy protocol that allows multiple routers to share a virtual IP address and provide a backup gateway for hosts.

In simple words

- VRRP works like HSRP but can run on routers from different vendors (Cisco, Juniper, HP).  
- One router is the **Master**, and others are **Backup**.

---

###  How VRRP Works
- Routers share one virtual IP.  
- The router with the highest priority becomes **Master**.  
- All other routers act as Backup routers.  
- If the Master fails → a Backup becomes the new Master automatically.  
- Works across multiple vendors (multi-vendor support).

---

###  Why VRRP Is Used?
- For networks with mixed devices  
- Redundancy across different brands  
- Faster failover compared to HSRP  

---

## 3. GLBP (Gateway Load Balancing Protocol)

GLBP is a Cisco protocol that provides both router redundancy and load balancing by allowing multiple routers to actively forward traffic at the same time.

In simple words

- GLBP is different from HSRP and VRRP.  
- Instead of one router working and others waiting, **all routers can share the traffic**.

---

###  How GLBP Works

- Routers form a GLBP group.  
- They use one **virtual IP**, like HSRP and VRRP.  
- GLBP assigns **multiple virtual MAC addresses**.  
- Each host gets a different virtual MAC address.  
- Traffic is distributed across all routers.  
- If one router fails → remaining routers continue forwarding traffic.

---

###  Why GLBP Is Used?
- Provides load balancing across multiple routers  
- Provides redundancy at the same time  
- All routers are used efficiently (no idle router)

---

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

---

##  Simple One-Line Definitions

**HSRP:** Cisco protocol where one router is Active and another is Standby, providing gateway redundancy.

**VRRP:** Open-standard redundancy protocol similar to HSRP, but supports multi-vendor routers.

**GLBP:** Cisco protocol that provides redundancy and load balancing by allowing multiple routers to forward traffic together.

---


##  Firewalls in Corporate Networks

###  What is a firewall?

A **firewall** is a security device (hardware or software) placed between:

- The **internal network (LAN)**, and  
- The **outside world (internet or other networks)**

It monitors and controls traffic based on rules.

> A firewall works like a **security guard** at the main gate of a company.

It checks:

- Who is coming in?
- Who is going out?
- Are they allowed?

---

###  Why do companies use firewalls?

- To block **unauthorized access**
- To allow only required services (HTTP, HTTPS, SSH, etc.)
- To protect against attacks (malware, hackers, port scans)
- To create different security zones:
  - Internal LAN
  - DMZ (public servers)
  - Internet

---

###  Types of Firewalls (Simple View)

#### **Packet-Filtering Firewall**
- Checks source IP, destination IP, port, and protocol.
- Uses simple ACL rules.
- Works at Network & Transport layers.

#### **Stateful Firewall**
- Remembers connection states.
- Understands new, established, and related connections.
- More secure than packet-filtering.

#### **Application Layer / Next-Gen Firewall (NGFW)**
- Understands applications like Facebook, WhatsApp, YouTube.
- Can filter by user identity.
- Offers IPS/IDS, deep packet inspection, URL filtering.

#### **Host-Based Firewall**
- Runs on individual devices (e.g., Windows Defender Firewall).

---

###  Simple Firewall Rule Example

A small company firewall may have rules like:

- Allow outgoing HTTP/HTTPS from LAN to Internet.
- Allow incoming HTTPS only to the web server in DMZ.
- Block Telnet (port 23) everywhere.
- Deny all other traffic by default.

This ensures:

- Employees can browse safely.
- Customers can access the company website.
- Dangerous services are blocked.


