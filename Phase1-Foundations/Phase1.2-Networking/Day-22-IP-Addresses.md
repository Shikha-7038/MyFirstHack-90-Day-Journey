# 🌐 Day 22 — IP Addresses: Finding My Own IPs and Understanding What They Reveal

**Day 22 of 90 | MyFirstHack — Phase 1.2: Networks**

## 🎯 Today's Objective

Today I learned how **IP addresses identify devices on a network**, the difference between **private and public IP addresses**, how **NAT** allows private devices to access the internet, and how **ARP** connects IP addresses with MAC addresses on a local network.

I also performed practical exercises using my own laptop and the network I was connected to.

---

## 🧠 What I Learned

### 1. What is an IP address?

An **IP (Internet Protocol) address** is an address used to identify a device/interface on a network so that network traffic can reach the correct destination.

For IPv4, an address looks like:

```text
192.168.x.x
```

IPv4 uses **32 bits**, divided into four 8-bit numbers called octets. Each octet can have a value from `0–255`.

I also learned that an IPv4 address contains a **network part** and a **host part**. The subnet mask helps determine which part represents the network and which part identifies the device within that network.

---

## 🏠 2. Private IP vs Public IP

One important concept I learned today was that my laptop can have a **private IP** while websites see a **public IP**.

### Private IP

Private IP addresses are used inside local networks.

The three main private IPv4 ranges are:

```text
10.0.0.0 – 10.255.255.255
172.16.0.0 – 172.31.255.255
192.168.0.0 – 192.168.255.255
```

My laptop was using a private IP from the `192.168.x.x` range.

I learned that the same private IP can exist in many different networks. However, two devices cannot normally use the same private IP at the same time on the same local network because that would create an IP conflict.

---

## 🌍 3. Finding My Public IP

I checked my public IP while connected to a shared Wi-Fi network.

For privacy, I am **not recording my actual public IP** in this documentation.

The public IP is the address that external websites and services can generally see when my traffic reaches the internet.

---

## 🔄 4. NAT — Network Address Translation

I learned how my laptop can use a private IP while communicating with websites on the internet.

This is possible because of **NAT (Network Address Translation)**.

A simplified version is:

```text
My laptop
Private IP
      ↓
Local gateway/router
      ↓
     NAT
      ↓
Public IP
      ↓
Internet
```

The router translates between the private address used inside the network and the public address used outside.

I initially found it confusing how multiple devices could appear to use the same public IP without receiving each other's data. I learned that NAT keeps track of individual connections, including information such as ports, so returning traffic can be associated with the correct internal device.

---

## 📱 5. NAT and CGNAT

I also learned about **CGNAT (Carrier-Grade NAT)**.

Normal NAT can allow many devices inside one network to share a public IP.

With CGNAT, an ISP can also allow **multiple customers or networks to share public IPv4 addresses**.

This helped me understand why seeing the same public IP does not necessarily mean that multiple devices are actually the same device or belong to the same person.

---

## 🚀 6. IPv4 and IPv6

IPv4 provides approximately:

```text
4.3 billion addresses
```

This became insufficient as the number of internet-connected devices increased.

IPv6 was introduced as the long-term solution. IPv6 uses **128-bit addresses**, providing an extremely large number of possible addresses.

Example:

```text
2001:db8:85a3::8a2e:370:7334
```

I learned that many modern devices support both IPv4 and IPv6, which is called **dual-stack**.

---

# 🔎 Practical Task 1 — Finding My Own IPs

## Private IP

I used Windows Command Prompt and ran:

```text
ipconfig
```

I found my laptop's private IPv4 address.

For privacy, the exact address is **not included in this public documentation**.

## Public IP

I used an IP lookup service to find the public IP visible to the internet.

For privacy, I have **not recorded the actual public IP**.

The lookup provided information such as:

- Country
- Region
- Approximate city
- ISP/organization
- VPN/proxy-related classification

---

# 🔍 Practical Task 2 — Comparing IP Lookup Services

I checked the same public IP using **two different IP lookup services**.

The most interesting result was that the services did **not completely agree**.

The public IP and country were consistent, but the estimated location and organization information differed.

One service associated the IP with one approximate location and classified it as a residential proxy, while the other provided a different location/organization and did not show a VPN/proxy indication.

### 💡 What I learned

> **IP geolocation is an estimate, not an exact GPS location.**

Different databases can have different information about the same IP address.

This means that someone who knows an IP address cannot automatically determine someone's exact physical location from the IP alone.

---

# 🔐 7. What a Public IP Reveals

I learned that a public IP can provide information such as:

### Usually available or inferable

- 🌍 Country
- 📍 Approximate region/city
- 🏢 ISP or network organization
- 🔐 Possible VPN/proxy/hosting classification

### Not directly revealed by the IP alone

- ❌ My name
- ❌ My exact street address
- ❌ Everything I am doing online
- ❌ A complete identity of the person using the connection

The IP becomes more useful as a security signal when combined with other information such as:

```text
IP + Login time + Account + Location + Device information
```

For example, a login from an unusual country or network can trigger additional verification.

---

# 🔗 Practical Task 3 — Understanding ARP

I used the Windows command:

```text
arp -a
```

to examine my laptop's ARP cache.

I found a **dynamic IP-to-MAC mapping for my local network gateway**.

For privacy, I have intentionally **not included the actual gateway IP or MAC address** in this public documentation.

In simple terms, ARP helped my laptop associate:

```text
Local IP address
      ↕
MAC address
```

This allows communication with the gateway on the local network.

---

## 🧩 What I Found in the ARP Output

The ARP output contained more than just device entries.

I also saw multicast and broadcast addresses. I initially thought these might represent additional devices.

I learned that they are **multicast or broadcast addresses**, not individual laptops or phones.

This was an important lesson because simply seeing an address in `arp -a` does not mean:

> "This is another device connected to my network."

---

# ⚠️ Important Scope Lesson

The original exercise was designed for a **home network**, where I could safely identify my own devices.

I was actually connected to a **shared Wi-Fi network**, so I did not attempt to discover or investigate other people's devices on the network.

Instead, I limited my practical work to information available from **my own laptop and its ARP cache**.

I also learned that:

> **An ARP cache is not necessarily a complete list of every device on a network.**

It only contains the mappings that my computer currently knows about.

---

# 🧠 My Key Findings

### Finding 1 — IP geolocation can differ

Two services checked the same public IP but produced different location/organization information.

**Lesson:** IP geolocation is approximate.

### Finding 2 — My private IP is not my public IP

My laptop had a **private IP**, while websites generally saw a **public IP**.

**Lesson:** NAT connects private addressing with public internet communication.

### Finding 3 — ARP does not show every network device

My ARP cache contained a dynamic mapping for my local gateway and several special multicast/broadcast entries.

**Lesson:** `arp -a` shows the ARP information my computer currently has; it is not a guaranteed inventory of every device on the network.

---

# 🔐 Security Connection

Today I started seeing IP addresses from a **defender's perspective** instead of only treating them as networking terminology.

An IP address can be used for:

- 🌐 Routing traffic
- 📍 Approximate geolocation
- 🏢 Identifying an ISP/network
- 🔐 Detecting unusual login activity
- 🚨 Supporting security alerts
- 🔎 Investigating network activity

At the same time, I learned not to overinterpret an IP address.

An IP is **not automatically a person's identity or exact physical location**.

---

# 📝 Final Takeaway

Before today, I mostly thought of an IP address as just a number assigned to a device.

Now I understand that there are several layers to it:

```text
Private IP
    ↓
Local Network
    ↓
Gateway
    ↓
NAT
    ↓
Public IP
    ↓
Internet
```

I also learned that:

> **IP addresses tell networks where to send traffic, but they can also become security signals when combined with other information.**

The most useful practical lesson for me was that **tools and databases need interpretation**. The IP lookup services gave different location results, and the ARP output contained addresses that were not individual devices.

That made the networking concepts feel much more real than simply reading their definitions.

---

## 🚀 Day 22 Complete

**Topics covered:**

- ✅ IPv4
- ✅ Private vs public IP
- ✅ Subnet/network and host concepts
- ✅ NAT
- ✅ CGNAT
- ✅ IPv6
- ✅ Public IP and geolocation
- ✅ IP as a security signal
- ✅ ARP
- ✅ IP-to-MAC mapping
- ✅ Multicast and broadcast addresses
- ✅ Network assessment scope

**Next:** 🚪 **Day 23 — Ports: How One Computer Can Run Many Network Conversations at Once**
