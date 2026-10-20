# 🌐 Day 7 – DNS Deep Dive & Week 1 Reflection

**📅 Date:** 30 July 2026

---

## 🎯 Objective

Go beyond the basic idea of DNS and understand how DNS queries actually travel across the internet, why caching is essential, how DNS attacks work, and perform hands-on exercises using browser Developer Tools and `nslookup`.

---

## 📚 What I Learned

### 1️⃣ The Complete DNS Resolution Process

When I type a domain name like `google.com`, my computer doesn't immediately know its IP address. Instead, a sequence of systems work together to find it.

### Complete DNS Resolution Flow

```text
My Computer
      │
      ▼
Browser Cache
      │
      ▼
Operating System Cache
      │
      ▼
Router Cache
      │
      ▼
Recursive DNS Resolver
      │
      ▼
Root DNS Server
      │
      ▼
Top-Level Domain (TLD) DNS Server
      │
      ▼
Authoritative DNS Server
      │
      ▼
Recursive Resolver
      │
      ▼
My Computer
```

### 💡 My Understanding

One thing that became much clearer today was the role of the **Recursive DNS Resolver**.

Initially, I thought the Root DNS Server directly contacted the TLD Server, and then the TLD Server contacted the Authoritative Server.

I learned that this is incorrect.

The **Recursive Resolver** is responsible for asking each DNS server one by one.

The process actually looks like this:

```text
My Computer
      │
      ▼
Recursive Resolver
      │
      ├──► Root DNS Server
      │        │
      │        └── "Ask the .com TLD Server"
      │
      ├──► TLD DNS Server
      │        │
      │        └── "Ask Google's Authoritative DNS Server"
      │
      ├──► Authoritative DNS Server
      │        │
      │        └── Returns Google's IP Address
      │
      ▼
My Computer
```

The Root DNS Server never contacts the next server itself. It only tells the Recursive Resolver where to go next.

---

## 🗂️ 2. DNS Caching

DNS responses are stored temporarily so the same lookup doesn't have to be repeated.

Caching occurs at multiple places:

- 🌐 Browser
- 💻 Operating System
- 📡 Router
- 🛰️ Recursive DNS Resolver

Each cache stores its own copy independently.

### ⏳ TTL (Time To Live)

Every DNS record includes a **TTL (Time To Live)** value.

TTL tells devices:

> "Keep this DNS record for this amount of time before asking again."

### 💡 My Understanding

I learned that:

- TTL is **not fixed**
- Every website owner decides its own TTL
- Different websites can use different TTL values
- Administrators can change TTL whenever needed
- Large companies like Google may return different IP addresses depending on:
  - User location
  - Server load
  - Availability
  - Traffic routing

---

## 🚀 3. Why DNS Caching Matters

Caching reduces the number of DNS requests across the internet.

Without caching:

- Every website visit would contact Root DNS Servers
- Then TLD Servers
- Then Authoritative DNS Servers

This would make the internet much slower.

### 🔒 Security Perspective

Caching improves performance but also creates a security risk.

If an attacker successfully poisons a DNS cache, every user relying on that cache receives the malicious IP address until the TTL expires.

---

## ⚠️ 4. DNS Attacks

### 🧪 DNS Cache Poisoning

The attacker tricks a Recursive Resolver into storing a fake IP address.

**Result**

Every user using that resolver is redirected to the attacker's website.

---

### 🎯 DNS Hijacking

Instead of changing cached records, the attacker changes which DNS server the victim uses.

Example:

```text
Google DNS (8.8.8.8)
        │
        ▼
Attacker-controlled DNS Server
```

Now every DNS request goes to the attacker's DNS server first.

---

### 📦 DNS Tunneling

Attackers hide stolen information inside DNS requests because DNS traffic is usually allowed through firewalls.

---

### 🎭 Typosquatting

Attackers register domains that closely resemble legitimate websites.

Examples:

```text
google.com
gooogle.com

paypal.com
paypa1.com
```

Users accidentally visit the fake website.

### 💡 My Understanding

I wondered whether **DNS Hijacking** and **DNS Cache Poisoning** could happen together.

The answer is **yes**.

For example:

1. The attacker hijacks the victim's DNS settings.
2. The malicious DNS server then returns fake IP addresses.

Both attacks work together to redirect victims.

---

## 🛠️ Practical Task 1 – Running DNS Queries

I used Windows Command Prompt and the `nslookup` command.

### Commands Used

```cmd
nslookup google.com

nslookup reddit.com

nslookup cnn.com

nslookup google.com 8.8.8.8

nslookup google.com 1.1.1.1
```

### 🔍 My Findings

- Google resolved to a different IP address than the example shown in the course.
- `cnn.com` returned multiple IPv4 and IPv6 addresses.
- Google's DNS and Cloudflare's DNS returned different valid IP addresses for the same domain.

### 💡 My Learning

Initially, I thought one website always had one IP address.

Now I understand that large websites use multiple servers around the world.

DNS may return different IP addresses depending on:

- Load balancing
- Geographic location
- Anycast routing
- DNS Resolver

---

## 🧪 Practical Task 2 – Observing DNS Caching

Using Chrome Developer Tools:

```text
F12
↓
Network
↓
Timing
```

I measured DNS lookup time.

### 📊 Results

| Test | DNS Lookup Time |
|------|----------------:|
| First Request (Disable Cache Enabled) | **363 ms** |
| Second Request (Cache Enabled) | **0 ms** |

### 👀 Observation

When browser caching was enabled, Chrome reused the cached DNS record.

No new DNS query was required.

This practical task helped me understand why DNS caching makes websites load faster.

---

## ❓ Additional Questions I Explored

### 🌍 Public IP vs Private IP

I confirmed that:

- The ISP assigns one **Public IP** to the router.
- The router assigns **Private IP** addresses to connected devices.
- NAT allows multiple devices to share one Public IP.

---

### 🏫 College Wi-Fi

I wanted to know whether people using the same Wi-Fi could identify exactly which person visited which website.

### 💡 My Understanding

- Websites only see the shared Public IP.
- They cannot identify the individual laptop.
- However, the network administrator can identify devices using internal network logs.

---

### 🔄 Different Networks Produce Different Results

I compared my college Wi-Fi with my mobile hotspot.

I learned that changing networks changes:

- Public IP
- Private IP
- DNS Server
- Route to websites

while the websites themselves remain the same.

---

## ✅ Key Takeaways

- The **Recursive Resolver** performs the DNS lookup by communicating with different DNS servers.
- DNS caching occurs at multiple layers and greatly improves internet performance.
- TTL controls how long cached DNS records remain valid.
- Large websites use multiple IP addresses for performance and availability.
- DNS attacks often exploit trust in DNS rather than attacking websites directly.
- `nslookup` and Chrome Developer Tools are valuable for understanding real DNS behavior.
- Performing practical experiments made networking concepts much easier to understand than theory alone.

---

## 💭 Week 1 Reflection

Completing the first week changed the way I think about the internet.

Instead of simply using websites, I now understand many of the steps happening behind the scenes—from DNS resolution and IP addressing to routing, caching, and browser requests.

The hands-on exercises with `tracert`, `nslookup`, and Chrome Developer Tools connected the theory with real-world networking, making these concepts much easier to understand.

---

## 🎯 Conclusion

Day 7 strengthened my understanding of one of the internet's most important services—DNS. I learned that DNS is much more than a simple "phonebook of the internet." It is a distributed system that relies on recursive queries, caching, and multiple layers of servers to resolve domain names efficiently.

By combining theory with practical exercises, I gained a clearer understanding of how DNS works in real-world environments, why caching is essential for performance, and how attackers can exploit weaknesses through techniques like cache poisoning, hijacking, tunneling, and typosquatting.

This lesson also reinforced the importance of verifying concepts through hands-on practice rather than relying only on diagrams or theoretical explanations.