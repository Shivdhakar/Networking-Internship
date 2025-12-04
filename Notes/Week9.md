# Subnetting
Subnetting is the process of dividing one large IP network into smaller, manageable networks called subnets.
It helps organize the network, improve security, reduce broadcast traffic, and use IP addresses more efficiently.

Simple line:
Subnetting = Breaking one network into many smaller networks.

This helps in:
- Better network organization
- Improved security (separate departments / teams)
- Reducing broadcast traffic
- Saving IP addresses

Think of subnetting like dividing a big class into smaller groups so things stay organized and easier to manage.


## How Subnetting Works 

An IP address has two parts:

| Part | Meaning |
|------|--------|
| Network part | Identifies the network |
| Host part | Identifies the devices inside that network |

When we subnet, we **take some bits from the host part** and use them to create more networks.

Example idea:  
A /24 network has 256 IPs.  
If we break it into 4 equal subnets, each gets 64 IPs.


##  Example of Subnetting

Original network:  
`192.168.1.0/24` (256 total IP addresses)

We want **4 smaller subnets**.

Result after subnetting (/26 each):

| Subnet | Network Address | Broadcast Address | Usable IP Range |
|--------|-----------------|------------------|----------------|
| 1 | 192.168.1.0 | 192.168.1.63 | 192.168.1.1 – 192.168.1.62 |
| 2 | 192.168.1.64 | 192.168.1.127 | 192.168.1.65 – 192.168.1.126 |
| 3 | 192.168.1.128 | 192.168.1.191 | 192.168.1.129 – 192.168.1.190 |
| 4 | 192.168.1.192 | 192.168.1.255 | 192.168.1.193 – 192.168.1.254 |


##  Key Points to Remember

- Subnetting = dividing a big network into small networks  
- Helps save IP addresses  
- Reduces traffic and increases security  
- Uses a **subnet mask** to define subnet size (example: `/26`, `/28`)

---
<br/>

#  CIDR (Classless Inter-Domain Routing)

CIDR is a method of representing and allocating IP addresses using a prefix / notation (like /24, /26) instead of old Class A/B/C system.
It allows flexible network sizes and prevents wastage of IP addresses.

Simple line:
CIDR = A way to write and manage IP ranges using /prefix for flexibility.
Example:  
`192.168.1.0/24`

The `/24` means **24 bits are network bits**, and the rest are hosts.


##  Why CIDR is Used

Before CIDR, we had fixed classes:

| Class | Default Mask | Size |
|------|--------------|------|
| A | /8 | Very large networks |
| B | /16 | Medium networks |
| C | /24 | Small networks |

This caused **wastage of IP addresses**.

CIDR solves this by letting us choose **any size network**, not only /8, /16, /24.


##  How CIDR Works (Simple Logic)

CIDR lets us select how many bits are used for the network portion.

Examples:

| CIDR | Subnet Mask | Usable Hosts |
|------|-------------|--------------|
| /24 | 255.255.255.0 | 254 hosts |
| /26 | 255.255.255.192 | 62 hosts |
| /28 | 255.255.255.240 | 14 hosts |

So instead of using fixed classes, we can choose `/24`, `/25`, `/26`, etc.



##  CIDR Example

Given network: `10.0.0.0/16`

We can divide it into smaller subnets like:

- `/24` → 256 addresses each  
- `/26` → 64 addresses each  
- `/28` → 16 addresses each  

CIDR = **flexible network sizing**, depending on requirement.

---

##  Subnetting vs CIDR

| Topic | Meaning |
|-------|--------|
| Subnetting | Breaking a large network into smaller networks |
| CIDR | A method to represent IP ranges and subnet size using `/notation` |

**Easy to remember:**  
- Subnetting = cutting  
- CIDR = naming those cuts efficiently

---

##  Summary


| Concept | Simple Meaning |
|--------|----------------|
| Subnetting | Dividing a large network into small networks |
| CIDR | Flexible method of writing and managing IP networks (/value) |

<br/>

#  Load Balancer

A **load balancer** is a network device or software that distributes incoming traffic across multiple servers so no single server gets overloaded.  
Its main goal is to keep applications fast, reliable, and always available.

In simple words:  
> Load balancer acts like a traffic policeman that directs user requests to different servers so all servers share the work.


##  Why Load Balancer is Used?

- Avoid overloading a single server  
- Improve performance and speed  
- Increase reliability and uptime  
- Provide backup if one server fails  
- Scale applications for more users  



##  How It Works (Simple Explanation)

Imagine 5 people asking the same question to only 1 teacher — the teacher will get tired.  
If 5 teachers are available and each student goes to a different one — faster results.

Similarly:

1. User sends a request  
2. Load balancer receives the request  
3. It checks healthy servers  
4. It forwards the request to the most suitable server  
5. If one server fails, it sends traffic to others  



## Load Balancing Methods (Algorithms)

| Method | Meaning |
|--------|--------|
| **Round Robin** | Requests go to each server one by one |
| **Least Connections** | Sends traffic to the server with the fewest open connections |
| **IP Hash** | Client IP decides which server it connects to |
| **Weighted Round Robin** | Stronger servers get more requests |



##  Types of Load Balancers

| Type | Description |
|------|------------|
| **Hardware Load Balancer** | Dedicated physical device (used in big data centers) |
| **Software Load Balancer** | Installed on servers (Nginx, HAProxy, Traefik) |
| **Cloud Load Balancer** | Provided by cloud services (AWS, Azure, GCP) |


##  Where Load Balancers Are Used?

- Websites and web applications  
- Cloud platforms  
- Banking systems  
- E-commerce websites  
- High-traffic online services  

Examples: Amazon, Google, YouTube, Flipkart all use load balancers.





