## HSRP

HSRP means Hot Standby Router Protocol. It is used when we have two or more routers and we want only one router to work as the main router. The other router stays in standby mode. If the main router stops working, the standby router becomes active automatically. This provides failover. HSRP works only on Cisco devices because it is Cisco proprietary. A virtual IP address is created and all computers use this IP as their gateway.

---

## VRRP

VRRP means Virtual Router Redundancy Protocol. It is almost similar to HSRP but it is an open standard. This means it works on different types of routers from different companies. VRRP also uses a virtual IP address. One router becomes the master and the others are backups. If the master router fails, a backup router takes over. VRRP provides fast failover and is widely used.

---

## GLBP

GLBP means Gateway Load Balancing Protocol. It is also Cisco proprietary. GLBP provides both router redundancy and load balancing. Multiple routers can work together and share traffic. GLBP creates multiple virtual MAC addresses. Different computers are given different MAC addresses, so traffic is divided between routers. If one router goes down, the others continue to work.

---

## Router Redundancy

Router redundancy means having backup routers in a network so that if one router fails, another router takes over. This prevents network downtime. Protocols like HSRP, VRRP, and GLBP help in providing redundancy. This is important in organizations where continuous network connectivity is required.

