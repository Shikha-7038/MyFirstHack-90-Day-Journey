# Day 30 — Proxies

**Day 30 of 90 · How Networks Actually Work**

---

## 🛡️ Today's Topic: Proxies

A **proxy** is a server that sits between a user and a destination on the internet.

Instead of:

```text
Your Device → Website
```

the communication can become:

```text
Your Device → Proxy → Website
```

The proxy receives the request, processes it according to its configuration, and forwards it to the destination.

### Common purposes of a proxy

- 🔍 Inspect traffic
- 🚫 Block unwanted websites or services
- 🛡️ Detect security threats
- 📝 Log network activity
- ⚡ Cache frequently requested content
- 🎯 Control which resources users can access

---

## 🔄 Proxy vs VPN

Both proxies and VPNs can place another server between a device and the destination, but they are not the same.

| VPN | Proxy |
|---|---|
| Usually handles most or all device traffic | Usually handles specific application traffic |
| Encryption is a central feature | Encryption depends on the proxy protocol |
| Often used for privacy or secure remote access | Often used for filtering, monitoring, and control |
| Commonly changes the visible IP | Can change the visible IP for the traffic it handles |
| Often user-controlled | Often organization-controlled |

### Simple way to remember

> 🔐 **VPN = encrypted tunnel**

> 🚦 **Proxy = traffic checkpoint/intermediary**

---

# 🧩 Types of Proxies

## 1. Forward Proxy

A **forward proxy** sits between users and the internet.

```text
Employee → Forward Proxy → Internet
```

Organizations can use forward proxies to:

- 🚫 Block websites
- 🔍 Inspect traffic
- 📝 Log activity
- ⚡ Cache content
- 🎯 Control internet access

A forward proxy is mainly concerned with **controlling users' outgoing traffic**.

---

## 2. Reverse Proxy

A **reverse proxy** sits in front of web servers.

```text
User → Reverse Proxy → Web Server
```

The user may think they are communicating directly with the website's server, but the reverse proxy handles the request first.

### Common purposes

- 🛡️ Protect backend servers
- ⚖️ Load balancing
- ⚡ Caching
- 🔐 TLS termination
- 🔍 Security inspection
- 📈 Handle large amounts of traffic

Services such as **Cloudflare** and **Fastly** can provide reverse-proxy/CDN infrastructure.

---

## 3. Transparent Proxy

A **transparent proxy** is a forward proxy that the user may not know is present.

The user does not necessarily configure their browser manually.

```text
User → Network → Transparent Proxy → Internet
```

It can be used by organizations, schools, hotels, or other networks for:

- Filtering
- Monitoring
- Access control
- Traffic management

---

# 🔍 What Proxies Actually Do

## 🚫 1. Content Filtering

A proxy can maintain rules for categories or destinations.

```text
User requests website
        ↓
Proxy checks policy
        ↓
Allowed → Forward request
Blocked → Reject request
```

If a request is blocked, the user may see a message such as:

> "Access denied by your administrator."

The organization configures the proxy to decide **when to block** and **which message to display**.

---

## 🛡️ 2. Security Inspection

Modern proxies can inspect traffic for:

- Malware
- Phishing
- Suspicious websites
- Command-and-control communication
- Possible data exfiltration

For HTTPS traffic, some organizations use **TLS interception**.

In a managed environment, the proxy can decrypt traffic, inspect it, and then encrypt it again before sending it onward.

This requires the organization's trusted certificate to be installed on managed devices.

---

## ⚡ 3. Caching

A proxy can store frequently requested content.

```text
User 1 → Proxy → Website
              ↓
          Save content

User 2 → Proxy → Cached content
```

This can reduce bandwidth usage and improve performance.

---

## 🕵️ 4. Anonymisation

Some proxies can hide the user's IP address from the destination.

However, a proxy should **not automatically be considered secure or private**.

An untrusted proxy operator may be able to see or modify traffic, depending on the protocol and encryption being used.

---

## ⚖️ 5. Load Balancing

Reverse proxies can distribute requests among multiple backend servers.

```text
                 → Server 1
Users → Proxy →  → Server 2
                 → Server 3
```

This prevents one server from receiving all the traffic.

---

## 🔐 6. TLS Termination

A reverse proxy can handle HTTPS/TLS connections on behalf of backend servers.

```text
User
 ↓ HTTPS
Reverse Proxy
 ↓
Backend Server
```

This can centralize certificate management and reduce the TLS workload on application servers.

---

# 👀 What Can a Proxy Log?

Depending on its configuration, a proxy can record information such as:

- 🌐 Destination/domain
- 🔗 URL or requested resource
- 🕐 Time of request
- 💻 User/device identity
- 📊 Amount of data transferred
- ✅ Allowed or blocked result
- ⚠️ Security events

Not every proxy logs everything.

> **Logging depends on how the proxy is configured.**

---

# 🚨 What Happens When a Request Is Blocked?

A simplified process is:

```text
User requests website/service
          ↓
      Proxy receives request
          ↓
      Check security policy
          ↓
     ┌────┴────┐
     ↓         ↓
  Allowed    Blocked
     ↓         ↓
 Forward       Reject
 request       request
```

The proxy can return a predefined response or blocking page when the request is denied.

Different blocking reasons can have different messages, for example:

- 🚫 Website blocked by policy
- ⚠️ Security threat detected
- 🔒 Restricted category
- 🛑 Access not permitted

---

# 🔎 Proxy and Phishing Protection

A proxy **can help protect users from phishing**, but it is not automatically a complete phishing defense.

For example:

```text
User clicks suspicious link
          ↓
Proxy receives request
          ↓
Checks destination/reputation
          ↓
Known malicious?
     ↓              ↓
   Yes              No
     ↓              ↓
  Block          Allow
```

A security proxy can compare destinations against threat-intelligence databases and security rules.

However, a phishing site that has not been identified yet may not be blocked.

> **Proxy = one layer of protection, not complete protection.**

---

# 🔄 Forward Proxy vs Reverse Proxy

The easiest way to remember the difference:

### Forward Proxy

**Protects or controls the users' side.**

```text
Users → Proxy → Internet
```

### Reverse Proxy

**Protects or handles the servers' side.**

```text
Internet → Reverse Proxy → Servers
```

---

# 🌐 Where Proxies Are Found

Proxies can exist in many environments:

- 🏢 Corporate networks
- 🏫 Schools and universities
- ☕ Public Wi-Fi networks
- 🏨 Hotels
- ☁️ Cloud environments
- 🌍 Large websites

You may use a proxy without realizing it.

---

# 🧪 Practical Task 1 — Checking for Proxies and Reverse Proxies

Today I performed three practical checks to understand how proxies can appear in real network communication.

---

## Test 1 — BrowserLeaks

I used BrowserLeaks to inspect my connection.

### With VPN enabled

The connection was identified as a **Proton AG VPN** network.

The apparent location and network were associated with the VPN server rather than my normal network.

### With VPN disabled

The connection was identified with my normal **Vodafone Idea** mobile network.

No explicit VPN or Tor relay was identified.

### What I learned

This demonstrated that a VPN can change the network identity visible to an external website.

It also showed why VPN and proxy detection should not be treated as exactly the same thing.

---

## Test 2 — Traceroute

I used the Windows command:

```text
tracert google.com
```

The first hop was:

```text
10.94.190.48
```

This is a private IP address.

Several intermediate hops returned:

```text
Request timed out.
```

However, the traceroute eventually reached Google's infrastructure.

### What I learned

Traceroute shows the network path through different hops, but it is **not a perfect proxy detection method**.

Some routers do not respond to traceroute probes because of firewall rules or configuration.

The first private IP suggested that my traffic first passed through an internal network gateway.

---

## Test 3 — Checking HTTP Response Headers

I inspected response headers from three websites to look for reverse-proxy or CDN fingerprints.

### 1. Cloudflare

I found headers including:

```text
cf-ray
cf-placement
```

These provided evidence that Cloudflare infrastructure was involved in handling the request.

### 2. Reddit

I checked the response headers but did not find an obvious reverse-proxy/CDN fingerprint such as:

```text
cf-ray
x-served-by
x-amz-cf-id
```

in the headers I examined.

This does **not** prove that Reddit does not use a reverse proxy or CDN. It only means that I did not find an obvious identifying fingerprint in the response headers I checked.

### 3. BBC

I found several strong indicators of Fastly/CDN infrastructure, including:

```text
x-served-by
x-cache
x-fastly-cache-status
via
req-svc-chain
```

For example:

```text
x-cache: HIT
x-fastly-cache-status: HIT-CLUSTER
```

These showed that cached content was being served through intermediary infrastructure.

---

# 🧠 What I Learned From the Practical

Before this practical, I mainly understood a proxy as a server between a user and a website.

After testing, I understood that proxies can serve very different purposes depending on where they are placed.

A **forward proxy** can control and inspect users' outgoing traffic, while a **reverse proxy** can protect and manage incoming traffic for web servers.

I also learned that reverse proxies and CDNs are common behind modern websites and can provide caching, performance improvements, load balancing, and security.

---

# 🔐 Trust and Privacy

A proxy creates an important trust relationship.

If traffic passes through a proxy, the proxy operator may be able to see or modify some of that traffic depending on the protocol, encryption, and configuration.

For example:

```text
User → Proxy → Website
```

The proxy is now an intermediary that needs to be trusted.

This is why it is important to understand **who controls the proxy** and **what it is configured to do**.

### Important examples

- 🏢 An employer may use a proxy to enforce security policies.
- ☕ A public network may use a transparent proxy for traffic management.
- 🌍 An untrusted public proxy may create privacy and security risks.
- 🌐 A website may use a reverse proxy/CDN to protect its servers.

---

# 📚 One-Month Network Summary

## 1. The Four-Part Conversation

Every network communication can be understood as a conversation between a sender and a receiver. For communication to happen, both sides need a common language (protocol) and a route through which the data can travel. This framework helped me understand networking concepts better because topics such as IP addresses, DNS, ports, TCP/UDP, and security controls became part of the same communication process instead of separate concepts.

## 2. How a Packet Actually Gets There

When I enter a website address in my browser, DNS first converts the domain name into an IP address so my device can find the correct destination. The IP address identifies the destination, while the port identifies the service, such as HTTPS on port 443. The communication then happens using protocols like TCP or UDP depending on the requirements. I also learned how private IP addresses are used inside local networks, public IP addresses are used for internet communication, and NAT allows multiple private devices to share a public IP.

## 3. The Controls That Shape the Network

Firewalls act as security checkpoints that control network traffic by allowing or blocking connections based on rules. VPNs create encrypted tunnels between a device and a VPN server and can change the visible public IP, while proxies act as intermediaries that can filter, inspect, cache, log, and control traffic. These technologies provide different layers of network security and management rather than performing exactly the same job.

## 4. One Thing I Can Do Now That I Couldn't on Day 21

I can now analyze network communication using practical tools. I can capture traffic using Wireshark and pktmon, read traceroute output to understand network paths, and identify reverse-proxy or CDN infrastructure by examining HTTP response headers.

## 5. One Thing I Still Find Confusing

I still want to understand enterprise network architecture more deeply, especially how different security controls such as firewalls, VPNs, NAT, and proxies work together in a real organization. I understand the individual purpose of each technology, but I need more practice visualizing the complete network design and traffic flow when multiple security layers are present.

---

# 📝 Reflection

### Approximate Time Taken

**30–40 minutes**

### Something I Can Do Now

I can analyze network paths and identify reverse-proxy or CDN infrastructure using practical tools and HTTP response headers.

### Something Still Confusing

I want to understand how multiple network security controls work together in a complete enterprise network architecture.

### Did Writing Reveal Any Gaps?

Yes. While writing the summary, I realized that I understand the overall flow of networking communication, but some areas such as the interaction between multiple security devices and deeper packet movement require more practice.

---

# 🎯 Key Takeaways

- 🔄 A proxy acts as an intermediary between endpoints.
- 🚦 Forward proxies primarily control users' outgoing traffic.
- 🛡️ Reverse proxies sit in front of servers and protect or manage incoming traffic.
- 👻 Transparent proxies can operate without the user manually configuring them.
- 🚫 Proxies can block websites and services according to policies.
- 🔍 Security proxies can inspect traffic for threats.
- ⚡ Proxies can cache content.
- ⚖️ Reverse proxies can perform load balancing.
- 🔐 Reverse proxies can handle TLS termination.
- 📝 Proxies may log network activity depending on their configuration.
- 🛡️ A proxy can help detect phishing, but it is only one security layer.
- 🌐 Large websites commonly use reverse-proxy/CDN infrastructure.
- 🔐 VPNs and proxies are related but serve different purposes.

> **A VPN mainly creates an encrypted tunnel, while a proxy acts as an intermediary that can control, inspect, filter, cache, or forward specific traffic.**

---

# 🚀 Day 30 Milestone

Thirty days of learning have helped me move from understanding basic digital concepts to analyzing real network behavior.

I can now connect networking concepts such as IP addresses, DNS, ports, TCP/UDP, firewalls, NAT, VPNs, and proxies into a larger picture and use practical tools to investigate network communication.

**30 days complete. 60 days to go. 🚀**