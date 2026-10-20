# 🛡️ MyFirstHack — Day 27: Firewalls

## 📅 Day 27 of 90

### 🎯 Topic
**Firewalls — how they control network traffic and protect systems**

---

## 🧠 What I Learned

Today I learned that a **firewall is a security control that allows or blocks network traffic based on rules**.

The basic idea is simple:

> **If traffic matches an allowed rule, it can pass. If it is not allowed, it can be blocked.**

I also learned that having a firewall does not automatically mean that a system is secure. A firewall is only **one layer of a defence-in-depth strategy**.

---

## 🔥 1. Types of Firewalls

I learned about four broad types of firewalls:

### 1. Packet-Filtering Firewall
- Examines packets individually.
- Mainly checks information such as:
  - Source IP
  - Destination IP
  - Destination port
  - Protocol
- It is fast and simple but does not track the state of connections.

### 2. Stateful Firewall
- Tracks active network connections.
- It remembers which conversations are already established.
- Reply packets belonging to an existing connection can be allowed back in.
- Unsolicited inbound packets can be blocked.

💡 **My understanding:** A stateful firewall is more aware of the context of a connection than a basic packet-filtering firewall.

### 3. Proxy Firewall
- Works as an intermediary between the client and destination.
- It accepts the client's connection and creates another connection to the destination.
- The internal system does not communicate directly with the outside system.

### 4. Next-Generation Firewall (NGFW)
- Goes beyond basic packet and connection inspection.
- Can use deep packet inspection and application awareness.
- It can make decisions based on the application and traffic content, not only the port.

---

## 📋 2. How Firewall Rules Work

Firewall rules are processed **from top to bottom**.

The important concept I learned is:

> **The first matching rule decides what happens to the traffic.**

For example:

```text
Rule 1: ALLOW → Web server → TCP 443
Rule 2: ALLOW → Web server → TCP 80
Rule 3: ALLOW → Office IP → TCP 22
Rule 4: DENY  → Any → Any
```

The final deny rule is called **default deny** or **implicit deny**.

### 🔐 Default Deny

The security principle is:

> **Only explicitly allowed traffic is permitted; everything else is blocked.**

This is safer than allowing everything and trying to block only known-bad traffic.

---

## ✅ 3. Allowlist vs Blocklist

### Allowlist / Whitelist
Only specifically approved traffic is allowed.

```text
Allow what is needed
        ↓
Block everything else
```

This generally provides stronger control but requires more administration.

### Blocklist / Blacklist
Known-bad traffic is blocked while other traffic is allowed.

```text
Block known-bad traffic
        ↓
Allow the rest
```

I learned that blocklists can be useful as an additional control, but they are generally not a replacement for a properly designed allowlist/default-deny approach.

---

## 🌐 4. Where Firewalls Are Used

Firewalls can be placed at different points in a network:

### 🌍 Perimeter Firewall
Located between the internal network and the internet.

### 🔒 Internal Segmentation Firewall
Separates sensitive parts of a network from general systems.

This can help limit **lateral movement** if one system is compromised.

### 💻 Host-Based Firewall
Runs directly on an individual device.

Examples include:
- Windows Defender Firewall
- Linux firewall mechanisms
- Built-in protections on modern devices

### ☁️ Cloud Firewall
Used to control traffic to cloud resources.

Examples include cloud security-group and firewall-rule systems.

### 🌐 Web Application Firewall (WAF)
A WAF focuses on web traffic such as HTTP/HTTPS.

It can inspect application-layer requests for patterns associated with attacks such as:
- SQL injection
- Cross-site scripting (XSS)
- Other web application attacks

---

## 🧱 5. Defence in Depth

One important idea from today's lesson was **defence in depth**.

A mature security architecture does not depend on only one firewall.

Different controls can protect different layers:

```text
Internet
   ↓
Perimeter Firewall
   ↓
Internal Network
   ↓
Internal Segmentation
   ↓
Host Firewall
   ↓
Application
```

For cloud and web applications, cloud firewalls and WAFs can provide additional layers.

💡 **My understanding:** If one security layer fails, another layer can still provide protection.

---

## ⚠️ 6. What Firewalls Cannot Do

This was one of the most important parts of today's lesson.

A firewall does **not** stop everything.

### 🚫 Allowed Traffic Can Still Be Dangerous

If malicious activity is sent through traffic that the firewall is configured to allow, a basic firewall may not recognize the attack.

For example, an attack against a web application can travel over allowed HTTPS traffic.

### 🔐 Encrypted Traffic

A firewall normally cannot see the contents of encrypted HTTPS traffic unless additional inspection is configured.

### 🎣 Social Engineering

A firewall cannot stop an employee from being tricked by a phishing message.

### 👤 Insider Threats

A person who already has legitimate access may be able to perform harmful actions without violating network firewall rules.

### 📤 Outbound Traffic

If an attacker has already compromised a machine, outbound connections may be allowed depending on the firewall's configuration.

💡 **My takeaway:** A firewall is **not a complete security solution**. It is one control within a larger security strategy.

---

# 🧪 Practical Task — Inspecting My Own Firewall

Today I inspected the firewall on my own **Windows laptop** using:

**Windows Defender Firewall with Advanced Security**

I did not change any rules. The task was observation only.

---

## 🔍 My Findings

### 🖥️ Operating System
**Windows**

### 🔥 Firewall
**Windows Defender Firewall with Advanced Security**

### 📋 Number of Rules
Hundreds of inbound rules were visible, but the interface did not display an exact total count.

I did not manually count them because an approximate count was sufficient for the task.

---

## 🔎 Specific Rule I Investigated

I selected a **Google Chrome** firewall rule.

| Setting | Finding |
|---|---|
| Application | Google Chrome |
| Enabled | Yes |
| Action | Allow |
| Protocol | UDP |
| Local Port | 5353 |
| Remote Port | All ports |

### 🧠 What I Understood From This

This helped me connect the theory to a real system.

Instead of a firewall simply being a single ON/OFF switch, Windows maintains individual rules that can control traffic for particular applications, protocols, and ports.

---

## 📥 Inbound and 📤 Outbound Defaults

I checked the default firewall behavior and found:

- **Inbound:** Block by default 🔒
- **Outbound:** Allow by default ✅

This helped me understand **default deny** in a real Windows environment.

An unsolicited inbound connection is generally blocked unless an appropriate rule allows it.

---

## 💡 My Personal Observation

Before this task, I knew that Windows had a firewall, but I had not looked closely at the individual rules.

What surprised me was that the firewall maintains **application-specific rules**, and a rule can be quite specific about the protocol and port being allowed.

Seeing a real Chrome rule made the concept of firewall rules much easier to understand than learning it only from theory.

---

# 📝 Key Takeaways

### 1️⃣ A firewall is a decision-maker
It evaluates network traffic against rules and decides whether to allow or block it.

### 2️⃣ Rule order matters
The first matching rule can determine the result.

### 3️⃣ Default deny is important
Unnecessary traffic should not automatically be trusted.

### 4️⃣ Stateful firewalls track connections
They can distinguish legitimate replies from unsolicited inbound traffic.

### 5️⃣ Firewalls exist at different layers
They can protect networks, individual hosts, cloud resources, and web applications.

### 6️⃣ Firewalls have limitations
They cannot replace endpoint security, access control, monitoring, secure applications, user awareness, and other security controls.

### 7️⃣ Theory becomes clearer when I inspect a real system
Looking at my own Windows firewall helped me connect concepts such as **allow rules, protocols, ports, inbound traffic, and default deny** with an actual configuration.

---

## 🎯 Final Takeaway

The biggest lesson for me today was:

> **A firewall is not a wall that makes a system secure. It is one security control that decides which network traffic is allowed or blocked.**

Understanding what a firewall can do — and equally important, what it cannot do — is essential for building a layered security approach.

---

## 📌 Task Status

- Learned the main firewall concepts
- Studied four major firewall types
- Learned how firewall rules are evaluated
- Understood default deny
- Compared allowlists and blocklists
- Learned different firewall placements
- Learned the limitations of firewalls
- Inspected my own Windows firewall
- Investigated a real application-specific rule
- Recorded inbound/outbound default behavior
- Did not modify any firewall rules

**63 days left. 🚀**

#MyFirstHack #Cybersecurity #Firewalls #NetworkSecurity #WindowsSecurity #LearningInPublic
