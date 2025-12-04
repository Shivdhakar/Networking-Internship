# VPN (Virtual Private Network) 

## 1. What is a VPN?

VPN stands for **Virtual Private Network**.  
In simple words, a VPN is like a **secret and secure tunnel** on the Internet that connects your device to another network safely.  

- Data travels through the Internet, but because it is **encrypted**, nobody in the middle can easily read it.  
- You can imagine it like sending your message inside a **locked box** that only the correct person can open.

**Main benefits of a VPN:**
- Privacy (your IP address and data are hidden)  
- Security (hackers cannot read your traffic easily)  
- Protection on public Wi‑Fi (cafes, airports, etc.)

<br/>

## 2. Why do we use a VPN?

### 1. Privacy and Security
- VPN encrypts internet traffic so that any attacker only sees unreadable data.  
- While using public Wi‑Fi, a VPN makes the connection much safer.

### 2. Work From Home / Remote Work
- Employees can securely access **office servers and files** from home.  
- It feels as if they are sitting inside the office network.

### 3. Connecting Branch Offices
- Example: **Delhi Office ⇄ VPN ⇄ Jaipur Office**  
- Both offices can share files and applications safely over the Internet.

### 4. Partner / Vendor Access
- A company can give limited VPN access to vendors or partners so they can reach only specific systems.

### 5. Cost Saving
- Instead of buying expensive private leased lines, companies can use the normal Internet and create secure VPN tunnels on top of it.

<br/>

## 3. Types of VPN

### A. Site-to-Site VPN

A Site-to-Site VPN is a type of VPN that **securely connects one office network to another office network over the Internet**.

**Explanation:**  
- It is used to connect **two complete networks** (for example, head office network and branch office network).  
- Once configured on routers or firewalls, the tunnel is usually always on.  
- Users in both offices can communicate as if they are on **one big local network (LAN)**.

**Example to remember:**  
Two schools in different cities are connected by a **secret tunnel** so they can share files and data safely.

<br/>

### B. Remote Access VPN
  
Remote Access VPN is a VPN where **an individual user securely connects to a private network (like a company network) from a remote location**.

**Explanation:**  
- It connects a **single user device** (laptop, PC, phone) to the organisation’s network.  
- The user runs a VPN client, logs in, and then can use internal resources.  
- After connection, the user behaves as if they are **inside the office network**.

**Basic steps:**
1. User installs a VPN client/application.  
2. Logs in with **username + password + OTP**.  
3. The company gives a **virtual IP address**.  
4. User can now open internal servers, files, and applications.

**Example:**  
An employee opens Orphin Chemistry internal files from home using Remote Access VPN.

<br/>

### C. SSL VPN

SSL VPN is a **browser-based VPN that uses SSL/TLS (HTTPS) to provide secure remote access to internal resources**.

**Explanation:**  
- It uses the same security technology as **HTTPS websites** (SSL/TLS).  
- Users normally open a browser, visit an HTTPS VPN portal, log in, and then access internal web apps.  
- Because it runs in the browser, it is easy to use and does not always need heavy client software.

**How it works (simple flow):**
1. User opens a browser and goes to `https://vpn.company.com`.  
2. Logs in on the portal.  
3. Browser and VPN gateway create a **secure SSL/TLS tunnel**.  
4. User can access internal web applications, portals, etc.

<br/>

### D. MPLS / Provider VPN

MPLS / Provider VPN is a VPN where **a service provider builds a private network (MPLS cloud) to securely connect an organisation’s different branches**.

**Explanation:**  
- Used mainly by **large organisations and banks**.  
- The telecom or ISP creates and manages a **private wide area network** (MPLS).  
- Branches connect into this provider network instead of using the public Internet.  
- Because traffic stays inside the provider’s controlled network, it is considered secure and stable, often without extra encryption.

**Example:**  
Banks like SBI and HDFC use MPLS-based networks to connect their branches.

<br/>

## 4. SSL / TLS – What keeps VPN and HTTPS secure?

### What is SSL/TLS?

- **SSL (Secure Sockets Layer)** and **TLS (Transport Layer Security)** are technologies that secure websites and VPN connections.  
- Whenever you see `https://` in the browser address bar, it means SSL/TLS is active.

**SSL/TLS mainly does three things:**
- **Encryption:** Scrambles data so others cannot read it.  
- **Authentication:** Confirms that the server or website is genuine, not fake.  
- **Integrity:** Ensures data is not changed while travelling.

<br/>

### Why is SSL/TLS important?

- Without SSL/TLS, passwords, OTPs, and card details travel as **plain text**, which hackers can easily read.  
- With SSL/TLS, all data is **encrypted**, so even if someone captures it, it looks like random, useless characters.

<br/>

### HTTPS (SSL/TLS) 

1. **Client Hello:** The browser asks the server for a secure connection.  
2. **Server Certificate:** The server sends a digital certificate signed by a trusted Certificate Authority (CA).  
3. **Certificate Check:** The browser checks if the certificate is valid, not expired, and matches the domain.  
4. **Key Exchange:** The browser creates a **secret session key** and sends it encrypted using the server’s public key.  
5. **Secure Session:** Both browser and server now use the same secret key to encrypt and decrypt data.

Result:  
There is a **secure, encrypted channel** between the user and the server, so data stays protected.

<br/>

## 5. SSL VPN – Real life example

**Scenario:**  
An employee is at home and wants to open company resources.

**Flow:**
1. The user opens a browser.  
2. Types `https://vpn.orphinchemistry.com`.  
3. The VPN gateway sends its SSL certificate.  
4. The browser checks the certificate and builds a secure HTTPS connection.  
5. The user logs in with **username + password + OTP**.  
6. After login, the user can access internal web pages, files, servers, CRM, and databases.

All traffic goes through a **fully encrypted tunnel**, so even if someone intercepts it, they cannot understand the data.

---

## 6.  revision table 

| Term                  | Simple meaning                                      |
|-----------------------|-----------------------------------------------------|
| **VPN**               | Secure, private tunnel over the Internet            |
| **Site-to-Site VPN**  | Connects one office network to another office network |
| **Remote Access VPN** | Employee connects securely to office from home      |
| **SSL VPN**           | Browser-based VPN using SSL/TLS (HTTPS)             |
| **MPLS / Provider VPN** | Private WAN built by ISP to connect branches     |
| **SSL/TLS**           | Technology that encrypts and secures connections    |
| **HTTPS**             | Secure version of HTTP using SSL/TLS                |
