# VPN and Tunneling

## 1. What is a VPN?

VPN stands for Virtual Private Network.<br/>
Simple meaning: VPN creates a secure and private tunnel over public Internet so that I or any office can talk safely.<br/>

Real example: I am sitting in a café using public Wi‑Fi and I open my bank account. Without VPN, a hacker on the same Wi‑Fi can see my password. With VPN, my data is encrypted so hacker only sees useless garbage.<br/>

How it works: My laptop → encrypted tunnel → VPN server → bank website. Nobody in between can read my data.<br/>

Key exam points:<br/>
I can say that VPN hides my real IP address and encrypts all my traffic.<br/>
VPN makes the public Internet feel like a private office network for me.<br/>

---

## 2. Types of VPN (With Examples)

### a) Site-to-Site VPN

Example: Head Office Delhi (100 employees) wants to connect with Branch Office Jaipur (50 employees).<br/>
How: Both office routers create an automatic VPN tunnel. Now a user in Delhi can open a shared folder in Jaipur as if the Jaipur office is in the next room.<br/>
Real use: For example, TCS Delhi and TCS Mumbai offices can use Site‑to‑Site VPN to share project files securely.<br/>

### b) Remote Access VPN

Example: A software engineer like me is working from home in Noida but needs to access the company server in Gurgaon.<br/>
How: I install Cisco VPN client, enter my username, password and OTP, I get a virtual IP, then I open company CRM as if I am sitting inside the Gurgaon office.<br/>
Real use: Companies like Wipro use Remote Access VPN when employees are working from home.<br/>

### c) SSL VPN

Example: A marketing manager is travelling to a client meeting in Bangalore and wants to check the sales dashboard.<br/>
How: She opens Chrome, types https://vpn.company.com, logs in and the dashboard opens securely in the browser.<br/>
Real use: Companies like Zoho or Freshworks use SSL VPN portals for remote workers.<br/>

### d) MPLS / Provider VPN

Example: A bank like SBI has many branches all over India.<br/>
How: A telecom provider like BSNL creates a private MPLS network that connects all SBI branches. Data from Mumbai branch goes to Delhi head office safely over this provider network.<br/>
Real use: Banks like HDFC and ICICI use MPLS VPN from providers like Airtel or Reliance to connect their branches.<br/>

---

## 3. VPN Protocols (With Examples)

### a) PPTP (Point-to-Point Tunneling Protocol)

Example: In old days like Windows XP time, small shops used PPTP for simple VPN connections.<br/>
Problem: The MS‑CHAPv2 security used in PPTP is weak and can be cracked easily, so it is not safe now.<br/>
Status: I only study PPTP for theory or history, I do not use it in real secure networks.<br/>

### b) L2TP/IPsec

Example: In Windows 10 I can create a VPN connection and choose L2TP/IPsec with pre‑shared key to connect to my office.<br/>
How: L2TP creates the tunnel and IPsec encrypts all the data inside that tunnel.<br/>
Real use: Many government offices and colleges still use L2TP/IPsec for remote access.<br/>

### c) IPsec (Tunnel Mode)

Example: A Cisco ASA firewall in Delhi office connects to another Cisco ASA in Mumbai office.<br/>
How: Both firewalls create an IPsec tunnel so that all office‑to‑office traffic is automatically encrypted.<br/>
Real use: Big companies like Infosys or Accenture use IPsec tunnels to connect their branches securely.<br/>

### d) SSL VPN

Example: I open https://vpn.orphinchemistry.com in any browser, log in and my company HR portal opens inside that secure page.<br/>
Advantage: I do not need heavy software, it even works from hotel Wi‑Fi or cyber café, I just need a browser.<br/>
Real use: Most remote access VPN solutions today are SSL based.<br/>

### e) OpenVPN

Example: Many commercial VPN apps like NordVPN or ExpressVPN use OpenVPN protocol in the background.<br/>
How: OpenVPN creates a secure tunnel over ports like 443 (HTTPS), so even strict firewalls allow it because it looks like normal web traffic.<br/>
Real use: When I use a public VPN service on my phone or laptop, it is very common that OpenVPN is running internally.<br/>

---

## 4. VPN Security Features (With Examples)

### 4.1 Encryption

Example: I send password=12345 through the network. Without encryption, a hacker sees password=12345 in clear text. With AES‑256 encryption, the hacker only sees something like random characters which do not make sense.<br/>
Common: VPNs mostly use strong algorithms like AES‑128 or AES‑256 which are used even in banking systems.<br/>

### 4.2 Authentication

Example: When I connect to my office VPN, the server asks for my username, my password and an OTP from Google Authenticator on my phone.<br/>
Methods: This can be simple username password, password plus OTP, smart card, fingerprint or certificate based login depending on the company security level.<br/>

### 4.3 Integrity

Example: Suppose my salary value is 50000 in a packet. A hacker tries to change it to 500000 while the packet is travelling. Integrity check using a hash like SHA‑256 fails and that packet is dropped, so the change does not reach the server.<br/>

### 4.4 Anti-Replay

Example: A hacker captures my valid login packet at 10 AM and tries to send the same packet again at 1 PM. VPN checks the sequence number and timing and sees it as an old packet, so it rejects it and my account is not misused.<br/>

---

# Tunneling – Student Notes (With Examples)

## 1. What is Tunneling?

Simple definition: Tunneling means putting one network packet inside another packet and sending it across a network.<br/>

Real example: My office uses IPv6 inside, but my ISP only supports IPv4. My IPv6 packet is put inside an IPv4 packet, then sent through ISP. At the other end, the IPv4 cover is removed and the original IPv6 packet comes out and is delivered.<br/>

Visual: I write a letter (original data). I put this letter inside a bigger envelope (tunnel packet). The post office reads only the outer envelope and delivers it. The receiver opens the outer envelope and reads my original letter.<br/>

---

## 2. Tunneling Protocols (With Examples)

### a) GRE (Generic Routing Encapsulation)

Example: An ISP wants to carry a customer’s VLAN or routing information through its main IP network. The customer traffic is wrapped inside GRE packets and carried over the ISP IP backbone, then unwrapped at the destination.<br/>
Real use: Many MPLS and ISP networks use GRE tunnels internally to move customer traffic.<br/>

### b) L2TP

Example: I connect using DSL at home. My PPP session from modem is carried inside L2TP across the ISP network to the main authentication server.<br/>
Real use: Broadband providers like BSNL or Airtel can use L2TP to transport user sessions inside their core network.<br/>

### c) IPsec Tunnel Mode

Example: A router in Delhi sends a packet from 192.168.1.10 to 192.168.2.20 in Jaipur. IPsec adds a new outer header with source Delhi public IP and destination Jaipur public IP and protects the whole original packet inside.<br/>
Real use: Enterprises use IPsec tunnel mode to connect branch networks securely over the Internet.<br/>

---

## 3. Tunneling Process (Complete Example)

Scenario: A PC in Delhi office with IP 192.168.1.10 wants to ping a server in Jaipur office with IP 192.168.2.20 over the Internet.<br/>

Step 1: Encapsulation at Delhi router:<br/>
The PC creates a normal IP packet from 192.168.1.10 to 192.168.2.20. The tunnel endpoint at Delhi takes
