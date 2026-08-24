# Day 33 — Network Attacks: Detection and Defence

## 📅 MyFirstHack — Day 33 of 90

## 🎯 Learning Objective

Today I learned about common network attacks and how malicious traffic can be recognised through network analysis.

The focus was on **detection and defence**, not performing attacks.

The main attacks and concepts covered were:

- Man-in-the-Middle (MITM)
- ARP Poisoning / ARP Spoofing
- DNS Spoofing
- Denial-of-Service (DoS)
- Distributed Denial-of-Service (DDoS)
- SYN Floods
- Packet Sniffing
- Network attack detection using Wireshark

---

# 1. The Main Idea — Network Attacks Abuse Trust

A major idea from today's learning is that many network attacks abuse the **default trust built into network protocols**.

Some protocols were designed when networks were considered more trustworthy than they are today.

For example:

- ARP trusts information about IP-to-MAC mappings.
- DNS relies on responses that provide domain-to-IP information.
- Unencrypted communication can be observed or modified by someone who gains access to the communication path.

Attackers can take advantage of this trust.

Modern security therefore focuses on:

- 🔐 Encryption
- ✅ Verification
- 🧱 Network segmentation

The basic principle is:

> Do not trust network information blindly. Verify identities, protect communication, and limit what an attacker can reach.

---

# 2. Man-in-the-Middle (MITM)

## What is MITM?

A **Man-in-the-Middle attack** occurs when an attacker positions themselves between two communicating parties.

### Normal communication

```text
Client → Server
```

### MITM communication

```text
Client → Attacker → Server
```

The attacker can potentially observe or modify communication depending on the security protections in use.

## Possible consequences

A MITM position can potentially allow an attacker to:

- Observe traffic
- Attempt to collect sensitive information
- Modify traffic
- Inject malicious content
- Monitor communication patterns

## Defence

Proper encryption and identity verification make MITM attacks much harder.

HTTPS uses TLS to:

- Encrypt communication
- Help verify the identity of the server through certificates

Certificate warnings should not be ignored blindly because they can indicate that the connection cannot be properly verified.

---

# 3. ARP Poisoning

## What is ARP?

**ARP stands for Address Resolution Protocol.**

On a local network, a device may know another device's IP address but need its MAC address to communicate with it at the Ethernet layer.

ARP helps discover this relationship.

For example:

```text
IP Address → MAC Address
192.168.1.1 → AA:BB:CC:DD:EE:FF
```

A device can broadcast a question such as:

```text
Who has 192.168.1.1?
```

The device using that IP can respond with its MAC address.

## The security problem

ARP does not provide strong built-in authentication for these claims.

An attacker on the same local network may attempt to send false ARP information.

For example:

```text
Router IP → Attacker's MAC Address
```

The victim may then send traffic through the attacker's device.

This can create a Man-in-the-Middle position.

## Possible ARP poisoning indicators

In a packet capture, an analyst may look for:

- Unexpected ARP replies
- Unrequested ARP responses
- The same IP address being associated with multiple MAC addresses
- A device's MAC address suddenly changing
- Wireshark warnings such as duplicate IP address detection

## Defences

- Secure local network access
- Separate guest and internal networks
- Network segmentation
- Dynamic ARP Inspection on managed switches
- Encryption to limit the impact of intercepted traffic

---

# 4. DNS Spoofing

## What is DNS?

**DNS stands for Domain Name System.**

DNS translates human-readable domain names into IP addresses.

For example:

```text
www.example.com
        ↓
IP address
```

## What is DNS spoofing?

DNS spoofing occurs when a victim receives a false DNS answer.

### Normal

```text
bank.example → Legitimate IP address
```

### Spoofed

```text
bank.example → Attacker-controlled IP address
```

The victim may then connect to the wrong server.

A convincing fake website could potentially be used to trick the victim into providing information.

## Possible DNS spoofing indicators

An analyst can look for:

- DNS responses from unexpected sources
- Unexpected IP addresses
- Multiple conflicting answers to the same DNS query
- Domain resolutions that do not make sense for the service

## Defences

### DNSSEC

**DNSSEC** adds cryptographic signatures to DNS records so DNS responses can be validated.

### DNS over HTTPS

**DoH** encrypts DNS communication using HTTPS.

### DNS over TLS

**DoT** encrypts DNS communication using TLS.

### HTTPS

HTTPS provides another layer of protection through TLS encryption and certificate validation.

The different layers reinforce each other.

---

# 5. Denial-of-Service (DoS)

A **Denial-of-Service attack** attempts to overwhelm a target so that legitimate users cannot access the service normally.

A simple example:

```text
Large amount of traffic
          ↓
       Server
          ↓
Resources exhausted
          ↓
Legitimate users affected
```

The goal is availability disruption rather than necessarily stealing information.

---

# 6. Distributed Denial-of-Service (DDoS)

A **DDoS attack** is a distributed form of DoS.

Instead of traffic coming from one source, many compromised devices may generate traffic toward the target.

These compromised devices can form a **botnet**.

```text
Device ──┐
Device ──┤
Device ──┤
Device ──┤ → Target Server
Device ──┤
Device ──┘
```

Because the traffic comes from many sources, the attack can be more difficult to block.

## Defence

DDoS protection can involve:

- Traffic filtering
- Rate limiting
- Reverse proxies
- Distributed infrastructure
- Dedicated DDoS protection services

---

# 7. SYN Flood

TCP normally establishes a connection using the three-way handshake:

```text
Client → SYN
Server → SYN-ACK
Client → ACK
```

A SYN flood abuses this process by generating many connection attempts without properly completing them.

This can cause a server to maintain many half-open connections and consume resources.

## Possible indicators

An analyst may observe:

- Very large numbers of SYN packets
- Many incomplete TCP connections
- A high volume of connection attempts
- Traffic from many sources in a distributed attack

A high number of SYN packets alone does not prove an attack. The overall pattern and context matter.

---

# 8. Packet Sniffing

**Packet sniffing** means capturing and examining network traffic.

Wireshark is a legitimate tool for packet capture and analysis.

However, capturing traffic that you are not authorised to monitor can be a privacy and security violation.

## Why encryption matters

On an unencrypted connection, captured packets may expose readable information.

With properly encrypted communication:

```text
Application Data
      ↓
Encrypted traffic
      ↓
Packet capture
      ↓
Content is not directly readable
```

A packet capture may still reveal metadata such as:

- Source and destination information
- Timing
- Packet sizes
- Connection patterns

The widespread use of encryption has therefore greatly reduced the usefulness of passive sniffing for directly reading sensitive application data.

---

# 9. Wireshark Detection Lab

Today's practical lab focused on identifying what **normal network traffic looks like**.

The purpose was to establish a baseline that could later help identify abnormal traffic.

Only my own traffic and network were captured.

---

## Step 1 — ARP Analysis

### Filter used

```text
arp
```

### Observation

The capture contained only two ARP packets.

The first was an ARP request:

```text
Who has 10.94.*.*? Tell 10.94.190.48
```

The second was the corresponding ARP reply:

```text
10.94.*.* is at c4:75:ab:3c:f2:71
```

This showed a normal request-and-response pattern.

### Result

- One ARP request was observed.
- One corresponding ARP reply was observed.
- No IP address was observed being claimed by multiple MAC addresses.
- No obvious ARP poisoning indicator was observed in this capture.

### Important limitation

This does not prove that the network is completely free from ARP poisoning. It only means that no obvious duplicate IP-to-MAC pattern was observed during this particular capture.

---

# 10. Step 2 — Wireshark Expert Information

I opened:

```text
Analyze → Expert Information
```

### Result

There were **no Expert Information entries** in this capture.

Wireshark did not report any expert events for this capture.

### Important limitation

A lack of Expert Information does not guarantee that the network is completely safe. It only means that Wireshark did not generate Expert Information entries for the traffic captured.

---

# 11. Step 3 — DNS Analysis

### Filter used

```text
dns
```

### DNS traffic observed

The capture contained queries for domains including:

```text
www.google.com
beacons.gcp.gvt2.com
```

The Google DNS traffic followed a normal query-response pattern.

Example:

```text
10.94.190.131 → 10.94.190.48
DNS query for www.google.com

10.94.190.48 → 10.94.190.131
DNS response for www.google.com
```

The response returned multiple IP addresses in the `142.251.x.x` range.

Multiple addresses are not automatically suspicious because large services can use multiple IP addresses for availability and load distribution.

The domain:

```text
beacons.gcp.gvt2.com
```

was not manually requested during the browsing activity, demonstrating that normal background services can generate DNS queries.

### Result

- Recognisable domains were observed.
- Background service activity was observed.
- DNS responses came from the observed DNS server.
- No obvious conflicting DNS responses were observed in the packets examined.
- No obvious DNS spoofing indicator was identified.

---

# 12. Step 4 — TCP SYN and RST Analysis

## Initial TCP connection attempts

### Filter used

```text
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

### Result

The capture contained:

```text
58 SYN packets
```

These represented initial TCP connection attempts.

The traffic was mainly associated with:

```text
Port 53
Port 80
Port 443
```

These are common service ports.

## TCP reset packets

### Filter used

```text
tcp.flags.reset == 1
```

### Result

The capture contained:

```text
1 RST packet
```

## Rough ratio

```text
58 SYN : 1 RST
```

This was the baseline observed in the normal capture.

There was no obvious pattern of repeated SYN attempts across many different ports on a single destination.

---

# 13. What Attack Patterns Would Look Like?

## ARP Poisoning

Possible signature:

```text
Unexpected ARP replies
        +
Same IP associated with different MAC addresses
        +
Possible changes in IP-to-MAC mappings
```

## DNS Spoofing

Possible signature:

```text
Unexpected DNS response source
        +
Suspicious or unexpected IP address
        +
Conflicting DNS answers
```

## SYN Flood

Possible signature:

```text
Very large number of SYN packets
        +
Many incomplete connections
        +
Potentially many different sources
```

## DDoS

Possible signature:

```text
Unusually high traffic volume
        +
Many sources
        +
Target service becoming unavailable
```

## Packet Sniffing

Packet sniffing itself can be difficult to identify from the victim's traffic alone because it can be passive.

Encryption is therefore an important defence because captured traffic becomes much less useful for directly reading sensitive information.

---

# 14. Key Detection Mindset

Today's practical exercise reinforced an important security-analysis principle:

> **You need to understand normal traffic before you can recognise abnormal traffic.**

Instead of only asking:

```text
"What protocol is this?"
```

a security analyst also asks:

```text
"Is this behaviour normal?"
```

For example:

### ARP

Instead of:

```text
"This is an ARP packet."
```

Ask:

```text
"Who is claiming this IP address?"
"Has this IP been associated with another MAC?"
```

### DNS

Instead of:

```text
"This is a DNS response."
```

Ask:

```text
"Who sent the response?"
"Does the answer make sense?"
"Are there conflicting answers?"
```

### TCP

Instead of:

```text
"This is a SYN packet."
```

Ask:

```text
"How many SYNs are being generated?"
"Are they targeting many ports?"
"Are connections completing normally?"
```

This is the shift from **packet recognition to security analysis**.

---

# 15. Key Lessons Learned

1. Network attacks frequently abuse trust built into protocols.
2. MITM attacks place an attacker between two communicating parties.
3. ARP poisoning abuses trust in IP-to-MAC mappings.
4. DNS spoofing abuses trust in DNS responses.
5. DoS and DDoS attacks focus on overwhelming services.
6. SYN floods can exploit TCP connection tracking.
7. Packet sniffing is passive traffic capture and becomes much less useful against properly encrypted traffic.
8. Encryption protects the confidentiality of network communication.
9. Verification helps detect impersonation and false information.
10. Network segmentation limits how far an attacker can move after gaining access.
11. Wireshark can help analysts identify unusual network patterns.
12. A baseline of normal traffic is essential for detecting anomalies.

---

# 🎯 Final Takeaway

The biggest lesson from Day 33 was:

> **You cannot recognise abnormal network behaviour unless you understand what normal behaviour looks like.**

Network attacks may look different, but many of them exploit **trust**.

The recurring defensive principles are:

```text
Encryption
    +
Verification
    +
Network Segmentation
    ↓
Stronger Network Security
```

Today's Wireshark exercise helped build a baseline for:

- ARP
- DNS
- TCP SYN
- TCP RST
- Wireshark Expert Information

The goal is not just to read packets anymore.

The goal is to **notice when something doesn't look right, investigate the pattern, and understand what it could mean**.

---

## 🧠 One-Sentence Summary

**Day 33 taught me that network attacks often abuse trust, and that understanding normal traffic in Wireshark is the foundation for recognising suspicious behaviour and defending networks.**
