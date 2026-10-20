# Day 29 — Virtual Private Networks (VPNs)

## 📅 Day 29 of 90

Today I learned about **Virtual Private Networks (VPNs)** and how they protect network traffic by creating an encrypted connection between a device and a VPN server.

I also performed a hands-on VPN inspection lab to observe how a VPN changes the public IP, apparent network location, DNS configuration, and network identity visible to websites.

The practical experiment also helped me understand what a VPN **does not** hide, such as account identity, cookies, and browser fingerprints.

---

## 🎯 Learning Objectives

- Understand what a VPN is
- Understand how a VPN tunnel works
- Learn how VPN encryption protects traffic
- Understand how a VPN changes the public IP visible to websites
- Understand how VPNs affect DNS
- Learn what a DNS leak is
- Understand network identity vs account identity
- Understand VPN vs HTTPS
- Learn what VPNs can and cannot protect
- Perform a practical VPN inspection
- Understand why a VPN does not provide complete anonymity

---

# 🔐 1. What is a VPN?

**VPN** stands for **Virtual Private Network**.

A VPN creates an **encrypted connection**, called a **VPN tunnel**, between a device and a VPN server.

Instead of traffic travelling directly from the device to the internet, it first travels through the VPN server.

### Without a VPN

```text
Device
   ↓
Wi-Fi / Network
   ↓
ISP
   ↓
Internet
   ↓
Website
```

### With a VPN

```text
Device
   ↓
🔐 Encrypted VPN Tunnel
   ↓
VPN Server
   ↓
Internet
   ↓
Website
```

The VPN server acts as an intermediary between the device and the websites being accessed.

---

# 🌐 2. What Happens When a VPN is Turned On?

When a VPN is connected:

1. The device establishes a connection with the VPN server.
2. An encrypted tunnel is created between the device and the VPN server.
3. Internet traffic travels through this tunnel.
4. The VPN server receives the traffic.
5. The VPN server forwards the request to its destination.
6. The website generally sees the VPN server's public IP address.
7. The response travels back through the VPN server and encrypted tunnel to the device.

The basic flow is:

```text
Device
   ↓
🔐 Encrypted Tunnel
   ↓
VPN Server
   ↓
Website
```

---

# 🔒 3. VPN Encryption

One of the main purposes of a VPN is to encrypt traffic between the device and the VPN server.

### Without a VPN

```text
Device ───────────────→ Internet
```

### With a VPN

```text
Device ═══ 🔐 ENCRYPTED ═══→ VPN Server
```

Someone monitoring the local network cannot simply read the contents of the encrypted VPN tunnel.

This can be particularly useful when using networks that are not fully trusted, such as:

- Hotel Wi-Fi
- Airport Wi-Fi
- Coffee-shop Wi-Fi
- Conference Wi-Fi
- Other public Wi-Fi networks

---

# 🌍 4. VPN and Public IP Address

A VPN can change the **public IP address visible to websites**.

### Without VPN

```text
Device
   ↓
Normal Network
   ↓
ISP
   ↓
Website
```

The website generally sees the public IP associated with the normal internet connection.

### With VPN

```text
Device
   ↓
🔐 Encrypted VPN Tunnel
   ↓
VPN Server
   ↓
Website
```

The website generally sees the VPN server's public IP instead.

This can also make the connection appear to come from a different network location.

### Practical observation

During today's practical experiment, connecting to a VPN changed the **network identity and location information visible to websites**.

---

# 👀 5. What Can Your ISP See?

Without a VPN, an ISP can generally observe information about the user's internet connections, including network destinations.

With a VPN:

```text
Device
   ↓
🔐 Encrypted VPN Tunnel
   ↓
VPN Server
```

The ISP can see that the device is connected to a VPN, but it normally cannot read the contents of the encrypted VPN tunnel.

However, this does **not** mean the traffic becomes completely invisible.

The VPN provider becomes another important trusted party because traffic eventually exits through the VPN provider's servers.

---

# 🧭 6. VPN and DNS

**DNS** stands for **Domain Name System**.

DNS converts domain names into IP addresses.

For example:

```text
example.com
     ↓
    DNS
     ↓
IP Address
```

DNS is an important part of VPN privacy because DNS requests can reveal information about the domains being requested.

During the practical experiment, I checked DNS using:

```text
nslookup example.com
```

Before connecting to the VPN, the laptop was using a local/private DNS server provided through the network.

After connecting to the VPN, the DNS configuration changed.

The DNS leak test also showed DNS servers associated with the VPN infrastructure.

After disconnecting the VPN, the DNS configuration returned to the normal local/private network setup.

---

# ⚠️ 7. What is a DNS Leak?

A **DNS leak** can happen when a device is connected to a VPN but DNS requests continue to use the normal ISP or network DNS server.

For example:

```text
VPN Connection
      ↓
Encrypted Traffic
      ↓
VPN Server
```

But DNS requests might accidentally take another path:

```text
DNS Request
     ↓
Normal DNS Server
     ↓
ISP / Network
```

This could reveal information about the domains being requested even while the VPN is active.

Therefore:

> **DNS routing is an important part of testing VPN privacy.**

---

# 🛡️ 8. What a VPN Does Well

A VPN can:

### 1. 🔐 Encrypt traffic

A VPN protects traffic between the device and the VPN server.

### 2. 👀 Change what the ISP can see

The ISP sees the VPN connection rather than the contents of the encrypted tunnel.

### 3. 🌍 Change apparent network location

Websites generally see the VPN server's IP and may associate the connection with the VPN server's location.

### 4. 🏢 Provide secure remote access

Organizations can use VPNs to allow employees to securely connect to internal company networks from outside the office.

---

# 🚫 9. What a VPN Does NOT Do

A VPN is **not a complete anonymity or cybersecurity solution**.

A VPN does not automatically:

- Make a person completely anonymous
- Protect against malware
- Protect against phishing
- Hide an account that the user logs into
- Remove cookies
- Prevent browser fingerprinting
- Replace HTTPS
- Replace strong passwords
- Replace MFA
- Provide complete cybersecurity protection

For example:

```text
Malware + VPN = Still Malware
```

A VPN protects the network connection, but it does not magically make malicious software safe.

---

# 👤 10. VPN Does Not Equal Anonymity

This was one of the most important concepts I learned today.

A VPN does not make observation disappear.

It **moves the trust boundary**.

### Without VPN

```text
You
 ↓
ISP
 ↓
Website
```

The ISP is one of the important parties that can observe network information.

### With VPN

```text
You
 ↓
VPN Provider
 ↓
Website
```

The VPN provider becomes another important trusted party.

Therefore:

> **A VPN changes who can see certain network information; it does not make observation disappear.**

---

# 🆔 11. Network Identity vs Account Identity

A VPN mainly changes **network identity**.

It can change information such as:

- Public IP
- Apparent location
- Network provider visible to websites
- Network path

However, a VPN does not automatically change:

- Google account
- Login credentials
- Cookies
- Browser settings
- Browser fingerprint
- Personal information

For example:

```text
VPN changes:
Public IP
Network location
Network path
```

But:

```text
VPN does not automatically change:
Google account
Cookies
Browser fingerprint
Login credentials
```

This explains why a website can see a different IP address while still knowing which account is logged in.

---

# 🔐 12. VPN vs HTTPS

VPN and HTTPS provide protection at different points.

### HTTPS

```text
Your Browser 🔐 Website
```

HTTPS protects the communication between the browser and the website.

### VPN

```text
Your Device 🔐 VPN Server
```

A VPN protects the connection between the device and the VPN server.

They can work together:

```text
Your Device
     ↓
🔐 VPN Encryption
     ↓
VPN Server
     ↓
🔐 HTTPS Encryption
     ↓
Website
```

Therefore:

> **A VPN does not replace HTTPS.**

---

# 🏢 13. VPN for Remote Work

Organizations commonly use VPNs to provide secure remote access.

For example, an employee working outside the office can connect to the company's VPN.

This can provide access to internal resources such as:

- Internal applications
- File servers
- Intranet services
- Corporate systems

The basic idea is:

```text
Employee Device
       ↓
🔐 VPN
       ↓
Company Network
       ↓
Internal Resources
```

---

# 🧪 14. Practical VPN Inspection Lab

## Objective

The purpose of the practical experiment was to compare the network **before, during, and after using a VPN**.

The experiment focused on:

- Public IP
- ISP
- Apparent location
- DNS configuration
- DNS leaks
- Account identity
- Cookies
- Browser fingerprinting

## Network Used

**Hostel Wi-Fi**

## VPN Used

**Proton VPN Free**

## VPN Server

A VPN server in **Norway** was used for the experiment.

---

# 📌 15. Step 1 — Baseline Before VPN

Before connecting to the VPN, I checked the public IP and ISP information.

I also checked the DNS configuration using:

```text
nslookup example.com
```

The DNS server shown was a local/private DNS server provided through the network.

This gave me a baseline to compare with the VPN connection.

---

# 📌 16. Step 2 — Connect to VPN

I connected my laptop to Proton VPN.

After the VPN connection was established, the VPN application showed that the connection was active.

An encrypted VPN tunnel was now being used between the laptop and the VPN server.

---

# 📌 17. Step 3 — Check Public IP After VPN

After connecting to the VPN, I checked the public IP information again.

The results showed that:

- The public IP had changed.
- The VPN provider was shown instead of the normal ISP.
- The connection appeared to originate from the VPN server's location.

This demonstrated that websites were seeing the **VPN server's network identity** rather than the original network identity.

---

# 📌 18. Step 4 — Check DNS After VPN

I ran:

```text
nslookup example.com
```

again after connecting to the VPN.

The DNS configuration changed to a private address associated with the VPN configuration.

I also performed a DNS leak test.

The test showed DNS servers associated with the VPN infrastructure.

The original ISP's DNS servers did not appear in the test.

This indicated that there was **no obvious DNS leak in this particular VPN configuration during the test**.

---

# 📌 19. Step 5 — Test Account Identity

While connected to the VPN, I opened Google in an Incognito window and logged into my usual Google account.

### Result

Google still recognized the account.

### Lesson

The VPN changed the network identity, but it did not hide the account identity.

```text
VPN changes → Network identity

VPN does not automatically change → Account identity
```

---

# 📌 20. Step 6 — Test Cookies and Existing Sessions

I also tested Google using the normal Chrome browser.

Google recognized the existing account/session.

### Result

The VPN did not remove existing cookies or login information.

This demonstrated that changing the public IP does not automatically make a browser session anonymous.

---

# 📌 21. Step 7 — Browser Fingerprinting

I used **EFF Cover Your Tracks** to examine browser tracking and fingerprinting.

The test showed that the browser had a **unique fingerprint**.

This demonstrated that:

> **Changing the IP address does not automatically eliminate browser fingerprinting.**

Websites can use browser and device characteristics to distinguish a browser even when the public IP changes.

---

# 📌 22. Step 8 — Disconnect VPN

Finally, I disconnected the VPN.

After disconnecting:

- The public IP returned to the normal network identity.
- The ISP information returned to the normal network.
- The apparent location returned to the normal network location.
- The DNS configuration returned to the local/private network setup.

This confirmed that the changes observed during the experiment were associated with the VPN connection.

---

# 🔎 23. Practical Observations

During the experiment, I observed that:

- Connecting to the VPN changed the public IP visible to websites.
- Websites saw the VPN provider instead of the normal ISP.
- The apparent network location changed.
- DNS configuration changed while the VPN was connected.
- The DNS leak test showed VPN-associated DNS servers.
- The original ISP's DNS servers did not appear in the test.
- Google still recognized my account.
- Existing browser sessions were still recognized.
- The browser still had a unique fingerprint.
- Disconnecting the VPN restored the normal network identity.

---

# 🧠 24. What I Learned Today

Today I learned:

- What a VPN is
- How a VPN tunnel works
- How VPN encryption protects traffic
- How a VPN changes the public IP visible to websites
- How a VPN can change apparent network location
- What an ISP can generally see when a VPN is used
- How DNS works with a VPN
- What a DNS leak is
- Why DNS testing is important
- What VPNs can and cannot protect
- Why a VPN does not provide complete anonymity
- The difference between network identity and account identity
- The difference between VPN encryption and HTTPS
- How VPNs can provide secure remote access
- How browser fingerprinting can still identify or distinguish a browser
- How to inspect VPN behavior using practical tests

---

# ⭐ 25. Key Takeaways

1. **A VPN creates an encrypted tunnel between a device and a VPN server.**
2. **Websites generally see the VPN server's IP instead of the original public IP.**
3. **A VPN can change the apparent network location.**
4. **A VPN can reduce what the local network and ISP can see inside the tunnel.**
5. **DNS routing is an important part of VPN privacy.**
6. **A DNS leak can expose DNS requests outside the VPN.**
7. **A VPN does not make a person completely anonymous.**
8. **A VPN does not hide account identity, cookies, or browser fingerprints.**
9. **HTTPS and VPNs protect different parts of the connection.**
10. **A VPN is one privacy and security tool, not a complete cybersecurity solution.**

---

# 🎯 Final Takeaway

The biggest lesson from Day 29 was that a VPN is **not a magic invisibility tool**.

It creates an encrypted tunnel, changes the network path, and can change the public IP and apparent location visible to websites.

However, it does not automatically hide account identity, cookies, or browser fingerprints.

> **A VPN changes your network identity and protects the connection to the VPN server, but it does not make you invisible online.**
