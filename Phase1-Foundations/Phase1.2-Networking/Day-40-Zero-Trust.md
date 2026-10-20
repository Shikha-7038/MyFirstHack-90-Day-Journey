# Day 40 — Zero Trust

## Topic
**Zero Trust Architecture and Principles**

## Objective

The objective of Day 40 was to understand the concept of Zero Trust, why traditional perimeter-based security models are no longer sufficient, and how Zero Trust principles can be applied to real network environments.

This lesson also connected several previously learned defensive concepts, including network segmentation, least privilege, firewalls, IDS/IPS, SIEM, logs, monitoring, and network forensics.

---

# What I Learned

## 1. Trust Can Be a Vulnerability

One of the main ideas behind Zero Trust is that attackers often exploit systems that trust something automatically.

Examples include:

- ARP poisoning, where devices may trust false ARP information.
- DNS spoofing, where systems may receive and trust malicious DNS responses.
- Man-in-the-middle attacks, where communication trust is abused.
- Lateral movement, where attackers take advantage of trusted internal network access.

Traditional networks often assumed that devices and users inside the network were trustworthy. Zero Trust challenges this assumption.

The core principle is:

> **Never trust automatically. Always verify.**

Being inside a network should not automatically provide access to resources.

---

# 2. The Castle-and-Moat Security Model

Traditional network security is often described as the **castle-and-moat model**.

The network perimeter acted like a castle wall:

- Firewalls protected the network edge.
- External users were considered untrusted.
- Internal users and devices were considered trusted.

This created a:

> **Hard shell, soft centre**

The outside perimeter could be strongly protected, but once an attacker entered the network, they could potentially move freely between internal systems.

---

# 3. Why the Traditional Model Broke

The traditional perimeter became less meaningful because modern organizations no longer operate entirely inside one physical network.

Several factors contributed to this change:

### Cloud Computing
Applications and data may now exist outside the organization's traditional network perimeter.

### Remote Work
Employees connect from homes, cafés, airports, and other locations.

### Mobile Devices
Many different devices connect to organizational resources from different locations.

### Phishing and Credential Theft
Attackers can gain access to internal systems through compromised accounts or devices.

The important lesson is:

> **Inside the network no longer means trustworthy.**

This is one of the main reasons Zero Trust became necessary.

---

# 4. The Five Principles of Zero Trust

## Verify Explicitly

Every access request should be authenticated and authorized.

Verification can consider:

- User identity
- Device
- Location
- Resource being accessed
- User permissions
- Suspicious or unusual behaviour

Strong authentication methods such as **Multi-Factor Authentication (MFA)** are important.

---

## Least Privilege

Users and devices should receive only the access they genuinely need.

This reduces the damage caused by a compromised account.

For example, an employee who only needs access to business files should not automatically have access to financial systems or customer databases.

Least privilege helps limit the **blast radius** of a security incident.

---

## Assume Breach

Zero Trust assumes that an attacker could already be inside the environment.

Instead of only focusing on preventing attackers from entering, security should also limit what an attacker can do after gaining access.

This leads to:

- Strong access controls
- Network segmentation
- Continuous monitoring
- Detection of suspicious behaviour

---

## Microsegmentation

Microsegmentation divides networks into smaller, controlled areas.

Instead of having one large trusted internal network, systems can be separated into smaller zones.

Examples include:

- Employee workstations
- File servers
- Finance systems
- Customer databases
- CCTV cameras
- IoT devices
- Guest Wi-Fi

Communication between these areas should be controlled and only allowed when necessary.

Microsegmentation makes **lateral movement more difficult**.

---

## Continuous Monitoring

Access should not be trusted permanently.

Even after access is granted, systems should continue monitoring for suspicious behaviour.

This connects directly to previously learned defensive technologies:

- IDS/IPS for detecting or blocking suspicious activity
- Logs for recording events
- SIEM for collecting and correlating security events
- Forensics for investigating incidents

Continuous monitoring allows organizations to identify suspicious activity even after a user has successfully authenticated.

---

# 5. Zero Trust in Practice

## Zero Trust Is a Journey

Organizations cannot switch to Zero Trust overnight.

Most existing organizations have:

- Legacy systems
- Existing networks
- Old applications
- Complex user access requirements

Therefore, Zero Trust is usually implemented gradually.

Organizations may begin by protecting their most sensitive resources and then expand Zero Trust principles to other systems.

Zero Trust should be viewed as an ongoing security journey rather than a project that is permanently completed.

---

# 6. Identity Becomes the New Perimeter

In traditional security, access was often based on location:

> "Are you inside the network?"

Zero Trust changes this to:

> "Who are you, and are you authorized to access this resource?"

Identity therefore becomes extremely important.

Important technologies include:

- **MFA — Multi-Factor Authentication**
- **IAM — Identity and Access Management**
- **SSO — Single Sign-On**

Access decisions are based more on verified identity and authorization than simply on network location.

---

# 7. The User Experience Challenge

Zero Trust can create problems if implemented poorly.

For example, requiring users to repeatedly authenticate during normal work could frustrate employees.

Frustrated users may:

- Search for workarounds
- Share accounts
- Ignore security controls
- Try to bypass security measures

A good Zero Trust implementation should balance strong security with a smooth user experience.

Additional verification should be requested when risk increases, such as:

- A new device
- An unusual location
- Suspicious activity
- Access to sensitive information

This approach provides stronger security without unnecessarily interrupting legitimate users.

> **Security that people route around is not effective security.**

---

# 8. Practical Zero-Trust Network Redesign Lab

I applied Zero Trust principles to redesign a fictional company network.

## Problems in the Original Network

The original company had several castle-and-moat assumptions:

- Employees logged in once using only a password.
- Employees on office Wi-Fi could access any internal system.
- Remote workers received full access after connecting through a VPN.
- CCTV and IoT devices shared the same network as employee workstations.
- The organization used one large internal network.
- The main firewall was located only at the network perimeter.

The major problem was that the company trusted users and devices based on their network location.

---

## Zero-Trust Redesign

### Authentication

Employees should use strong authentication, including MFA.

Access to sensitive systems should require appropriate identity and authorization checks.

---

### Least Privilege

Employees should only access resources required for their specific roles.

For example:

- Finance employees access finance systems.
- General employees access necessary business resources.
- Database administrators access database administration systems.

---

### Network Segmentation

The single large network should be divided into separate zones:

- Employee network
- File server network
- Finance systems
- Customer database
- CCTV network
- IoT network
- Guest Wi-Fi

Communication between these zones should be blocked by default and allowed only when necessary.

---

### Assume Breach

The company should operate under the assumption that a device or account could already be compromised.

A compromised employee device should not automatically provide access to finance systems or customer databases.

---

### Continuous Monitoring

The organization should use:

- IDS/IPS
- Centralized logging
- SIEM correlation
- Security monitoring
- Forensic investigation capabilities

These controls help identify and investigate suspicious activity.

---

# 9. Applying Zero Trust to a Small Business

Zero Trust principles can also be applied to smaller businesses without requiring expensive enterprise infrastructure.

For a small shop such as Maya's, three practical improvements are:

## Enable MFA

Enable Multi-Factor Authentication on important accounts, including:

- Business email
- Payment-related accounts
- Cloud services
- Important business applications

---

## Separate the Payment System

The payment system should be separated from:

- Employee devices
- CCTV systems
- IoT devices
- Customer Wi-Fi

This helps prevent attackers from easily reaching payment systems after compromising another device.

---

## Apply Least Privilege to Employees

Employees should receive access only to the systems required for their work.

They should not automatically receive administrator privileges or access to sensitive financial accounts.

---

# Key Connections to Previous Learning

Zero Trust connected several concepts learned throughout the Networks section.

| Previous Topic | Connection to Zero Trust |
|---|---|
| Firewalls | Default deny controls unnecessary traffic |
| Network Segmentation | Limits communication and lateral movement |
| Least Privilege | Limits unnecessary access |
| IDS/IPS | Detects and blocks suspicious activity |
| SIEM | Correlates security events |
| Logs | Record important security events |
| Forensics | Helps investigate incidents |
| Continuous Monitoring | Watches for suspicious activity after access |

---

# Key Takeaways

The most important lessons from Day 40 were:

1. **Trust can become a vulnerability when it is given automatically.**
2. **Being inside a network does not automatically mean a user or device is trustworthy.**
3. **Zero Trust is a security philosophy, not a single product.**
4. **Every access request should be verified appropriately.**
5. **Users should receive only the access they genuinely need.**
6. **Security should assume that a breach may already have occurred.**
7. **Microsegmentation helps limit lateral movement.**
8. **Continuous monitoring helps detect suspicious behaviour after access is granted.**
9. **Zero Trust is a gradual journey rather than an overnight implementation.**
10. **Strong security must also consider user experience.**

---

# Final Reflection

Day 40 helped me understand how many different defensive concepts connect together.

Network segmentation, least privilege, firewalls, IDS/IPS, SIEM, logs, monitoring, and forensics are not isolated security topics. They all contribute to a larger defensive strategy.

Zero Trust provides the strategic mindset that connects them:

> **Never trust automatically. Always verify. Assume breach. Limit the blast radius.**

This mindset applies not only to enterprise networks but also to smaller organizations through practical habits such as MFA, network separation, least privilege, and continuous monitoring.

Zero Trust is not just about building a stronger perimeter. It is about removing automatic trust and designing security so that even if an attacker gains access, their ability to move and cause damage is limited.

---

## Day 40 Complete

**Topic:** Zero Trust  
**Key Principle:** Never Trust, Always Verify  
**Practical Skills:** Zero-Trust Network Design and Security Reasoning  
**Main Outcome:** Understanding how modern defensive security concepts work together to verify access, assume breach, limit lateral movement, and reduce the blast radius of an attack.