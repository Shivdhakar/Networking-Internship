# VPN (Virtual Private Network) 

## 1. What is a VPN?

VPN stands for **Virtual Private Network**.  
In simple words, a VPN is like a **secret and secure tunnel** on the Internet that connects our device to another network safely.  

- Data travels through the Internet, but because it is **encrypted**, nobody in the middle can easily read it.  
- You can imagine it like sending your message inside a **locked box** that only the correct person can open.

**Main benefits of a VPN:**
- Privacy (your IP address and data are hidden)  
- Security (hackers cannot read your traffic easily)  
- Protection on public Wi‑Fi (cafes, airports, etc.)

<br/.

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

- Connects **two separate office networks** over the Internet.  
- Example: Head Office (Delhi) ⇄ VPN ⇄ Branch Office (Jaipur)  
- Routers or firewalls on both sides automatically create the VPN; employees do not have to connect manually.

We can remember it like this:  
Two schools in different cities are connected by a **secret tunnel** so they can share data safely.

<br/>

### B. Remote Access VPN

- Used by individual users like employees working from home or while travelling.

**Basic steps:**
1. User installs a VPN client/application.  
2. Logs in with **username + password + OTP**.  
3. The company gives a **virtual IP address**.  
4. Now the user behaves as if they are inside the office network.

Example:  
An employee opens Orphin Chemistry internal files from home using Remote Access VPN.

<br/>

### C. SSL VPN

- This VPN works through a **web browser using HTTPS (SSL/TLS)**, so it is very easy to use.

**How it works:**
1. User opens a browser and goes to `https://vpn.company.com`.  
2. User logs in.  
3. The browser creates a **secure SSL/TLS tunnel** with the VPN gateway.  
4. The user can access internal web applications, portals, etc.

**Why SSL VPN is popular:**
- No heavy software installation required.  
- Works from any normal browser.  
- Uses strong HTTPS encryption to protect data.

<br/>

### D. MPLS / Provider VPN

- Mostly used by **large organisations and banks**.  
- The Internet Service Provider (ISP) creates and manages a **private MPLS network** for the company.  
- Connections between branches are stable and reliable.

Because the whole network is private and controlled by the provider, usually extra encryption is not mandatory.  
Example: Banks like SBI and HDFC use MPLS-type networks to connect their branches.

---

## 4. SSL / TLS – What keeps VPN and HTTPS secure?

### What is SSL/TLS?

- **SSL (Secure Sockets Layer)** and **TLS (Transport Layer Security)** are technologies that secure websites and VPN connections.  
- Whenever you see `https://` in the browser address bar, it means SSL/TLS is active.

**SSL/TLS mainly does three things:**
- **Encryption:** Scrambles data so that others cannot read it.  
- **Authentication:** Confirms that the server or website is genuine, not fake.  
- **Integrity:** Makes sure data is not changed while travelling over the network.

---

### Why is SSL/TLS important?

- Without SSL/TLS, passwords, OTPs, and card details travel as **plain text**, which hackers can easily read.  
- With SSL/TLS, all data is **encrypted**, so even if someone captures it, it looks like random, useless characters.

---

### HTTPS (SSL/TLS) – Simple steps

1. **Client Hello:** The browser asks the server for a secure connection.  
2. **Server Certificate:** The server sends a digital certificate signed by a trusted Certificate Authority (CA).  
3. **Certificate Check:** The browser checks if the certificate is valid, not expired, and matches the domain name.  
4. **Key Exchange:** The browser creates a **secret session key** and sends it encrypted using the server’s public key.  
5. **Secure Session:** Both browser and server now use the same secret key to encrypt and decrypt data.

Result:  
There is a **secure, encrypted channel** between the user and the server, so data stays protected.

---

## 5. SSL VPN – Real life example

**Scenario:**  
An employee is at home and wants to open company resources.

**Flow:**
1. The user opens a browser.  
2. Types `https://vpn.orphinchemistry.com`.  
3. The VPN gateway sends its SSL certificate.  
4. The browser checks the certificate and then builds a secure HTTPS connection.  
5. The user logs in with **username + password + OTP**.  
6. After login, the user can access internal web pages, files, servers, CRM, and databases.

All traffic goes through a **fully encrypted tunnel**, so even if someone intercepts it, they cannot understand the data.

---

## 6. Quick revision table 

| Term                | Simple meaning                                      |
|---------------------|-----------------------------------------------------|
| **VPN**             | Secure, private tunnel over the Internet            |
| **Site-to-Site VPN**| Connects two office networks                        |
| **Remote Access VPN** | Employee connects to office from home            |
| **SSL VPN**         | Browser-based VPN using HTTPS                       |
| **MPLS**            | Private network created by ISP for organisations    |
| **SSL/TLS**         | Technology that encrypts and secures connections    |
| **HTTPS**           | Secure version of HTTP using SSL/TLS                |
