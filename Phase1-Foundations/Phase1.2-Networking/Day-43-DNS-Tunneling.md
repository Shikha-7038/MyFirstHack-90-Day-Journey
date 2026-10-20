# Day 43 — DNS Tunneling

**MyFirstHack 90-Day Cybersecurity Journey**  
**Day:** 43 of 90  
**Topic:** DNS Tunneling  
**Focus:** Understanding how attackers abuse DNS as a covert communication channel and how defenders can detect suspicious DNS behavior.

---

## 1. Objective

The objective of Day 43 was to understand **DNS tunneling**, why attackers use DNS to hide communication, what suspicious DNS tunneling looks like, and how defenders can detect it.

The practical exercise focused on **observation and analysis only**, using my own DNS traffic in Wireshark and provided examples.

---

## 2. What is DNS?

**DNS (Domain Name System)** translates human-readable domain names into IP addresses.

For example:

```text
google.com → DNS → IP address → Website
```

A simple way to understand DNS is:

> **DNS is like the Internet's phonebook.**

When a device needs to connect to a website or service, DNS helps it find the corresponding server.

Because DNS is essential to normal Internet communication, networks generally need to allow DNS traffic.

---

## 3. What is DNS Tunneling?

**DNS tunneling** is a technique where information is hidden or encoded inside DNS queries and responses.

Instead of sending information through an obvious communication channel, an attacker can place encoded information inside domain names or DNS records.

Example:

```text
x7f3k9q2bv8h4m1z.example.com
```

The unusual subdomain may contain encoded information that an attacker-controlled DNS server can interpret.

### Basic concept

```text
Compromised device
        ↓
Hidden/encoded information
        ↓
DNS query
        ↓
Network allows DNS
        ↓
Attacker-controlled DNS server
```

The same channel can potentially be used for communication in both directions.

---

## 4. Why Attackers Use DNS Tunneling

### Data Exfiltration

DNS tunneling can be used to move information from a compromised system to an attacker-controlled server.

```text
Victim → DNS queries → Attacker
```

### Command and Control

It can also be used as a communication channel between malware and an attacker-controlled system.

```text
Attacker ↔ DNS ↔ Compromised device
```

DNS tunneling is relatively slow because DNS queries can carry only limited amounts of information, but it can still be useful when other communication channels are restricted.

---

## 5. Why DNS is an Attractive Channel

The important idea is:

**DNS is necessary → DNS is trusted → DNS is allowed → DNS can be abused**

A network cannot simply block all DNS traffic without affecting normal applications and Internet access.

This connects directly to the security lesson from **Day 33**:

> **Attackers often abuse trust that protocols and networks provide by default.**

DNS tunneling takes advantage of the fact that DNS is expected and usually permitted.

---

# 6. Four Signs of Possible DNS Tunneling

## 6.1 Long and Random-Looking Domain Names

Normal DNS names are often short and recognisable:

```text
maps.google.com
api.stripe.com
cdn.shopify.com
```

Possible suspicious example:

```text
mw0rd4ta8x7zq3f9k2vn5b1c.example.com
```

DNS tunneling may create unusually long, random-looking, or encoded subdomains.

---

## 6.2 Abnormally High DNS Query Volume

DNS tunneling can carry only a small amount of information in each query.

Therefore, an attacker may need to generate many queries.

For example:

```text
Query 1 → small piece of data
Query 2 → small piece of data
Query 3 → small piece of data
Query 4 → small piece of data
...
```

A sudden increase in DNS activity can therefore be a useful detection signal.

However, there is no universal number of queries that automatically means tunneling. Analysts compare activity against the normal baseline for the environment.

---

## 6.3 Unusual DNS Record Types

Some DNS record types, particularly **TXT records**, can carry text.

Heavy or unusual use of TXT records to a particular domain can therefore be a potential indicator.

However:

> **An unusual TXT record alone does not prove DNS tunneling.**

The surrounding behavior and context are important.

---

## 6.4 Concentration on One Strange Domain

Another important indicator is repeated DNS communication with one unfamiliar domain.

For example:

```text
Computer
   ↓
abc123.strange-domain.com
   ↓
xyz789.strange-domain.com
   ↓
qwe456.strange-domain.com
   ↓
...
```

A device repeatedly making long, random-looking queries to one unusual domain is more suspicious than a single unusual DNS request.

---

# 7. Practical Exercise — Establishing a DNS Baseline

For the practical exercise, I used **Wireshark** to examine my own DNS traffic during normal browsing.

I captured DNS traffic and applied the filter:

```text
dns
```

During the capture, I observed approximately:

**188 DNS packets**

The domain names were generally:

- Short
- Recognisable
- Consistent with normal browsing activity

This established a baseline for what normal DNS traffic looked like on my system.

### My baseline

> **188 DNS packets during normal browsing, with generally short and recognisable domain names.**

This baseline is useful because detecting abnormal behavior requires an understanding of what normal behavior looks like first.

---

# 8. Analysis of Provided DNS Examples

I analyzed five example domains using the four tunneling indicators.

| Domain | Verdict | Reason |
|---|---|---|
| `maps.google.com` | Normal | Familiar and recognisable domain |
| `mw0rd4ta8x7zq3f9k2vn5b1c.datatunnel-c2.com` | Possible tunneling | Long, random-looking subdomain on an unfamiliar domain |
| `cdn.shopify.com` | Normal | Recognisable legitimate service |
| `aGVsbG8gd29ybGQgc2VjcmV0.exfil-node.net` | Possible tunneling | Encoded-looking subdomain on an unfamiliar domain |
| `api.stripe.com` | Normal | Recognisable API domain |

The suspicious examples were identified based on **patterns**, not simply because their names looked unusual.

---

# 9. Important Analyst Mindset

A single unusual DNS query does not automatically mean an attack.

For example, legitimate software can sometimes generate:

- Long domain names
- Random-looking strings
- Large amounts of DNS traffic
- TXT records

Therefore, a SOC analyst should ask:

- Is this normal for this device?
- How frequently are the queries occurring?
- Are the queries unusually long?
- Is one domain receiving most of the requests?
- Are unusual record types involved?
- What other events are occurring at the same time?

The correct mindset is:

> **“This behavior is unusual. Let's investigate.”**

rather than:

> **“This is definitely DNS tunneling.”**

---

# 10. Why DNS Cannot Simply Be Blocked

A simple solution would be:

> “DNS tunneling is dangerous, so block DNS.”

However, this isn't practical because DNS is essential for normal network communication.

Blocking DNS completely could prevent systems from resolving domain names and disrupt legitimate applications.

Therefore, the defensive approach is:

```text
Allow necessary DNS
        ↓
Monitor DNS activity
        ↓
Establish normal behavior
        ↓
Detect anomalies
        ↓
Investigate
        ↓
Respond
```

---

# 11. Defensive Tools

Day 43 connects directly to the defensive tools learned earlier in the Networks track.

### Day 32 — Network Analysis

Understanding normal DNS behavior makes unusual DNS activity easier to recognise.

### Day 36 — IDS

An **Intrusion Detection System (IDS)** can identify suspicious DNS patterns and known indicators.

### Day 37 — SIEM

A **SIEM** can correlate DNS activity with other security events and help identify patterns across multiple systems.

### Day 38 — Logs

DNS logs provide useful evidence such as:

- Timestamp
- Source device
- Requested domain
- Record type
- Response
- Frequency of requests

Together, these form a defensive detection process:

```text
DNS Logs
   ↓
IDS
   ↓
SIEM
   ↓
Investigation
   ↓
Response
```

---

# 12. Broader Security Lessons

DNS tunneling teaches several lessons that apply beyond DNS.

## Trust and Necessity Create Attack Surface

The things organizations **must allow** can become targets for abuse.

DNS is one example.

Other trusted channels can also potentially be abused, including:

- HTTPS
- Cloud services
- APIs
- Social media services

The technique changes, but the underlying principle remains:

> **Hide malicious activity inside traffic that looks legitimate.**

---

## You Can't Block Your Way to Security

Not every threat can be eliminated by blocking.

Some communication channels are necessary.

Therefore, security requires:

**Prevention + Detection + Response**

Not prevention alone.

---

# 13. Connection to Previous Learning

Day 43 brought together several concepts from the Networks track:

```text
Day 32
Normal DNS + Traffic Analysis
        ↓
Day 33
Network Attacks + Abuse of Trust
        ↓
Day 36
IDS
        ↓
Day 37
SIEM
        ↓
Day 38
Logs
        ↓
Day 40
Zero Trust
        ↓
Day 43
DNS Tunneling + Detection
```

The common security principle is:

> **Don't assume something is safe simply because it is trusted or allowed.**

---

# 14. Legal and Ethical Boundary

The practical exercise was limited to:

- My own DNS traffic
- My own machine
- Wireshark observation
- Provided example domains

DNS tunneling should only be studied or tested in systems that I own or have explicit authorization to test.

The goal of this exercise was **recognition and defensive detection**, not creating or deploying a tunnel against another network.

---

# 15. Key Takeaways

- **DNS** translates domain names into IP addresses.
- DNS is essential, which means networks generally need to allow it.
- **DNS tunneling** hides information inside DNS traffic.
- It can be used for **data exfiltration** and **command-and-control**.
- Four important detection indicators are:
  1. Long/random-looking domain names
  2. Abnormally high DNS query volume
  3. Unusual record types such as heavy TXT usage
  4. Concentration on one strange domain
- Establishing a **normal baseline** is important before identifying abnormal behavior.
- My normal browsing produced approximately **188 DNS packets**, with generally short and recognisable domain names.
- One unusual DNS query does not automatically prove malicious activity.
- DNS cannot simply be blocked because it is necessary for normal Internet communication.
- **Wireshark, IDS, SIEM, and logs** can work together to identify suspicious DNS behavior.
- Attackers can abuse other trusted channels, not just DNS.
- Security requires **prevention, detection, and response**.

---

## Final Reflection

Day 43 showed me that attackers do not always need a completely new or obviously malicious communication channel. They can abuse something that networks already trust and need.

DNS tunneling reinforced an important cybersecurity mindset:

> **You can't block your way to security. When something must be allowed, you need to understand its normal behavior, monitor it, detect anomalies, and investigate what doesn't belong.**

**Day 43 completed — DNS Tunneling.**