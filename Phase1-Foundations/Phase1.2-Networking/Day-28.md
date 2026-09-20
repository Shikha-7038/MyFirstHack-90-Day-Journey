# Day 28 — Network Address Translation (NAT)

## 📅 Day 28 of 90

Today I learned about **Network Address Translation (NAT)** and how it allows multiple devices on a private network to share a single public IPv4 address.

I also performed a hands-on NAT experiment using my Windows laptop and Android phone to see NAT working in practice.

---

## 🎯 Learning Objectives

- Understand what NAT is
- Understand why NAT is needed
- Learn the difference between private and public IP addresses
- Understand how a router translates private IP addresses
- Learn how PAT uses port numbers
- Understand the relationship between NAT and security
- Understand Carrier-Grade NAT (CGNAT)
- Understand why IPv6 reduces the need for NAT
- Perform a practical NAT experiment

---

# 1. What is NAT?

**NAT stands for Network Address Translation.**

NAT allows multiple devices on a private network to communicate with the internet using a shared public IPv4 address.

For example:

```text
Laptop ──┐
Phone  ──┤
TV     ──┤
Camera ──┘
     ↓
  Router
     ↓
    NAT
     ↓
One Public IP
     ↓
  Internet
```

Each device can have its own private IP address, while the router uses one public IP address to communicate with the internet.

---

# 2. Why is NAT Needed?

IPv4 addresses are **32 bits** long.

This provides approximately **4.3 billion possible IPv4 addresses**.

When IPv4 was designed, this seemed like a very large number. However, the number of internet-connected devices increased dramatically over time.

Eventually, public IPv4 addresses became scarce.

NAT helped solve this problem by allowing many devices to use private IP addresses internally while sharing a public IPv4 address externally.

### Simple idea

```text
Public IPv4 addresses → Limited

Private IP addresses → Reusable

NAT → Allows many private devices to share public IP addresses
```

---

# 3. Private IP Addresses

Three IPv4 ranges are reserved for private networks.

## 3.1 10.0.0.0/8

Range:

```text
10.0.0.0 – 10.255.255.255
```

Usually remembered as:

```text
10.x.x.x
```

---

## 3.2 172.16.0.0/12

Range:

```text
172.16.0.0 – 172.31.255.255
```

Usually remembered as:

```text
172.16–31.x.x
```

---

## 3.3 192.168.0.0/16

Range:

```text
192.168.0.0 – 192.168.255.255
```

Usually remembered as:

```text
192.168.x.x
```

Home networks commonly use addresses from this range.

For example:

```text
Laptop → 192.168.1.x
Phone  → 192.168.1.x
Router → 192.168.1.1
```

Different networks can reuse these private addresses because they are not directly routed across the public internet.

---

# 4. Private IP vs Public IP

A **private IP address** is used inside a local network.

A **public IP address** is used for communication with the wider internet.

For example:

```text
Laptop
Private IP
192.168.x.x
     ↓
Router
     ↓
Public IP
     ↓
Internet
```

The public internet normally sees the router's public IP rather than the laptop's private IP.

---

# 5. How NAT Works

Suppose a laptop has the private address:

```text
192.168.1.50
```

The laptop wants to access a website.

The traffic first goes to the router.

```text
Laptop
192.168.1.50
     ↓
  Router
     ↓
    NAT
     ↓
Public IP
     ↓
Internet
```

The router changes the source information from the private IP to its own public IP.

When the website sends a response, the router uses its NAT information to determine which internal device should receive the response.

Therefore:

```text
Private Device
      ↓
Router/NAT
      ↓
Public Internet
      ↓
Router/NAT
      ↓
Correct Private Device
```

---

# 6. NAT Translation Table

The router maintains a **NAT translation table** to keep track of connections.

A simplified example:

| Private Device | Destination | Public-Side Connection |
|---|---|---|
| Private IP + Port | Website IP + Port | Public IP + Port |
| Device A | Website A | Public IP + Port 1 |
| Device B | Website B | Public IP + Port 2 |
| Device C | Website C | Public IP + Port 3 |

When a response arrives, the router checks this table to determine which internal device should receive it.

---

# 7. PAT — Port Address Translation

The NAT method commonly used by home routers is **PAT (Port Address Translation)**.

It is also known as:

- **NAPT — Network Address Port Translation**
- **NAT Overload**

PAT allows many devices to share one public IP by using different port numbers for their connections.

For example:

```text
Laptop → Public IP : Port 60001
Phone  → Public IP : Port 60002
TV     → Public IP : Port 60003
```

The public IP is the same, but the port numbers allow the router to distinguish the different connections.

### Important concept

> **PAT is what allows many private devices to share one public IPv4 address at the same time.**

---

# 8. Static NAT

Another type of NAT is **Static NAT**, also called **1-to-1 NAT**.

In Static NAT:

```text
Private IP → Public IP
     1           1
```

Each private address is mapped to a dedicated public address.

This can be useful when a server needs to be consistently reachable using a particular public address.

Static NAT is less common in normal home networks.

---

# 9. NAT and Security

NAT was **not designed as a security control**.

Its main purpose was to conserve IPv4 addresses.

However, NAT has a useful security side effect.

## Unsolicited inbound connections

An external device generally cannot simply start a connection to a private device behind NAT because the router does not have a translation entry telling it where the traffic should go.

The router will generally drop such traffic.

```text
Internet
    ↓
Unsolicited connection
    ↓
Router/NAT
    ↓
Dropped
```

This provides some protection to devices behind the router.

---

# 10. NAT is Not a Firewall

NAT and firewalls are not the same thing.

### NAT

The main job of NAT is:

> **Translate network addresses and ports.**

### Firewall

The main job of a firewall is:

> **Control and filter network traffic according to security rules.**

Therefore:

```text
NAT ≠ Firewall
```

NAT can have a security benefit, but it should not be considered a replacement for a firewall.

---

# 11. NAT Does Not Stop Outbound Malware

Suppose malware infects a laptop and tries to contact an attacker's server.

```text
Laptop
   ↓
Router/NAT
   ↓
Internet
   ↓
Attacker's Server
```

Because the laptop initiated the connection, NAT can create a translation entry for that connection.

Therefore, NAT does not automatically detect or stop the malware.

This shows why other security controls such as firewalls and endpoint security are important.

---

# 12. Port Forwarding

NAT can make some legitimate inbound connections difficult.

For example, if someone wants to host a game server or web server from a home network, external users may not be able to connect directly to the internal device.

**Port forwarding** can be configured on the router.

Example:

```text
Internet
    ↓
Public IP + Specific Port
    ↓
Router
    ↓
Internal Device
    ↓
Server
```

Port forwarding tells the router which internal device should receive traffic arriving on a particular port.

---

# 13. UPnP

**UPnP stands for Universal Plug and Play.**

UPnP can allow devices to automatically request port forwarding from a router.

This is convenient because applications do not always require manual router configuration.

However, UPnP can also create security risks.

Malware on a network could potentially abuse UPnP to request that the router open a port.

Therefore, unnecessary UPnP can be a security concern.

---

# 14. NAT and Security Monitoring

NAT can create challenges for SOC analysts and incident responders.

Imagine an organization has many internal devices:

```text
100 Internal Devices
        ↓
       NAT
        ↓
One Public IP
        ↓
     Internet
```

A security log may show suspicious activity coming from the public IP.

However, the analyst still needs to determine:

> **Which internal device actually generated the traffic?**

NAT translation logs can help connect the public IP and port to the original private IP and port.

Without proper logging, identifying the affected device during an investigation can be much harder.

---

# 15. Carrier-Grade NAT (CGNAT)

**CGNAT stands for Carrier-Grade NAT.**

Some ISPs and mobile carriers use an additional layer of NAT.

Instead of only the home router performing NAT, the carrier can also translate addresses before traffic reaches the public internet.

```text
Device
   ↓
Private/Carrier Network
   ↓
CGNAT
   ↓
Shared Public IP
   ↓
Internet
```

This allows many customers to share public IPv4 addresses.

Because multiple customers can appear under the same public IP, blocking a public IP can sometimes affect innocent users as well.

---

# 16. NAT and IPv6

NAT became important mainly because IPv4 has a limited number of addresses.

IPv6 uses **128-bit addresses** instead of IPv4's 32-bit addresses.

IPv6 provides an enormous address space.

Because there are enough IPv6 addresses, NAT is generally unnecessary for conserving addresses.

With IPv6:

```text
Laptop → IPv6 Address
Phone  → IPv6 Address
TV     → IPv6 Address
Camera → IPv6 Address
```

Each device can have a globally routable address.

However, this does **not** mean every device should be accessible from the internet.

A firewall can still block unwanted incoming connections.

---

# 17. IPv4 and IPv6 Comparison

| Feature | IPv4 | IPv6 |
|---|---|---|
| Address size | 32-bit | 128-bit |
| Address space | Limited | Extremely large |
| NAT | Commonly used | Generally unnecessary |
| Private addressing | Common | Different addressing model |
| Security | NAT may provide an incidental inbound-blocking effect | Firewall explicitly controls traffic |

The transition from IPv4 to IPv6 is still ongoing, so many networks currently support both.

This is known as **dual-stack**.

---

# 🧪 18. Hands-on NAT Lab

## Objective

To prove that two devices on the same Wi-Fi network can have different private IP addresses while sharing the same public IP address.

## Devices Used

- Windows laptop
- Realme Narzo 60 5G Android phone

---

## Step 1 — Find the Laptop's Private IP

On Windows, I opened Command Prompt and ran:

```text
ipconfig
```

I checked the **IPv4 Address** under the Wi-Fi adapter.

The address started with:

```text
192.168...
```

This confirmed that the laptop was using a private IPv4 address.

---

## Step 2 — Find the Laptop's Public IP

I opened an online IP-checking website from the laptop.

The laptop showed a public IPv4 address.

For privacy, the complete public IP is not included in this documentation.

---

## Step 3 — Find the Phone's Private IP

I connected my Realme Narzo 60 5G to the **same Wi-Fi network** as the laptop.

I checked the phone's Wi-Fi network information and found a private IP beginning with:

```text
192.168...
```

The phone and laptop therefore had different private IP addresses.

---

## Step 4 — Find the Phone's Public IP

I opened the same IP-checking website on the phone while it was still connected to the same Wi-Fi.

The phone showed the **same public IP as the laptop**.

This was the main proof that NAT was working.

```text
Laptop ── Private IP ──┐
                      │
                      ↓
                   Router
                      ↓
                     NAT
                      ↓
                 Same Public IP
                      ↑
                      │
Phone ─── Private IP ─┘
```

---

# 📱 19. Bonus: Mobile Data and CGNAT

I then turned off Wi-Fi on my phone and enabled mobile data.

The phone showed a **different public IP** from the one it had used on Wi-Fi.

I also found an internal mobile-network address beginning with:

```text
10.194...
```

This helped demonstrate the concept of **Carrier-Grade NAT (CGNAT)** used by mobile networks.

The traffic can be represented as:

```text
Phone
   ↓
Mobile Carrier Network
   ↓
CGNAT
   ↓
Public IP
   ↓
Internet
```

---

# 🔎 20. Practical Observation

The most interesting observation from the lab was that my laptop and phone had different private IP addresses but appeared to the public internet using the same public IP when connected to the same Wi-Fi.

This made NAT much easier to understand because I was able to observe it using my own devices rather than only learning it theoretically.

---

# 🧠 21. What I Learned Today

Today I learned:

- What NAT means
- Why NAT was created
- Why IPv4 addresses became scarce
- The three private IPv4 address ranges
- The difference between private and public IP addresses
- How routers perform NAT
- How NAT translation tables work
- How PAT uses ports
- What Static NAT is
- Why NAT is not a firewall
- How NAT can block unsolicited inbound traffic as a side effect
- Why NAT does not stop outbound malware connections
- What port forwarding does
- What UPnP is and why it can be a security concern
- How NAT affects security monitoring and forensics
- What Carrier-Grade NAT (CGNAT) is
- Why IPv6 reduces the need for NAT
- How to practically observe NAT using two devices

---

# ⭐ Key Takeaway

> **NAT allows multiple devices with private IP addresses to share a public IPv4 address. It was created primarily to conserve IPv4 addresses, not as a security mechanism. NAT has a useful side effect of blocking many unsolicited inbound connections, but actual network security should be handled by firewalls and other security controls.**

---

## 🔗 Connection to Previous Learning

This topic connects several networking concepts I have learned during the journey:

```text
IP Addresses
      ↓
Private vs Public IP
      ↓
Routers
      ↓
Ports
      ↓
NAT
      ↓
PAT
      ↓
Firewalls
      ↓
Network Security
```

The hands-on experiment helped connect these concepts together and gave me a clearer understanding of what happens when devices communicate with the internet.