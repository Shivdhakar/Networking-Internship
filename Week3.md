# Switches – L2 and L3

## What is a Switch?
A switch is a network device that connects many PCs, servers, or other devices inside the same network (like a LAN).  
It sends the data only to the device that needs it (not to everyone), so it’s faster and safer than a hub.

---

## Layer 2 (L2) Switch
- Works on **Data Link Layer** of OSI model.  
- Uses **MAC address** to forward data.  
- Good for **LAN** connections like inside an office.

**Limit:**  
👉 Can’t talk between two different networks. Works only inside one network.

---

## Layer 3 (L3) Switch
- Works on **Network Layer** of OSI model.  
- Uses **IP address** to forward data.  
- Can **route** between different networks like a router.  
- Gives both **switching (L2)** + **routing (L3)** features.

**Use Case:**  
👉 Good for big networks where you need fast switching and also inter-network communication.

---

## L2 vs L3 Switch – Quick Compare

| Feature        | L2 Switch (Data Link) | L3 Switch (Network) |
|-----------------|-----------------------|---------------------|
| **Layer**       | Layer 2 (MAC)         | Layer 3 (IP)        |
| **Uses**        | MAC Address           | IP Address          |
| **Function**    | Switching in LAN      | Switching + Routing |
| **Speed**       | Faster, simple        | Slightly slower, more complex |
| **Example Use** | Office LAN            | Enterprise with VLANs |

---
