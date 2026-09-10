# Day 34 — Network Segmentation

## 📅 MyFirstHack — Day 34 of 90

### 🔐 Topic: Network Segmentation

---

## 📖 Overview

Network segmentation is the practice of dividing a network into smaller **zones or segments** and controlling communication between them.

The main purpose of segmentation is **containment**.

If one device is compromised, the attacker should not automatically be able to access every other device or system on the network.

The key idea is:

> **A breach does not have to become a total compromise.**

Segmentation limits an attacker's ability to move through the network and reduces the damage caused by a single compromised device.

---

# 1. 🌐 Flat Networks vs Segmented Networks

## Flat Network

A flat network is a network where many devices can communicate with each other with little or no separation.

For example:

```text
Laptop ───── Server
   │             │
   ├──── Camera  │
   │             │
   └──── Database
```

If the laptop becomes compromised, the attacker may have paths toward other systems.

This makes **lateral movement** easier.

---

## Segmented Network

A segmented network divides systems into different zones and places controls between them.

```text
User Zone
    │
    ↓
 Firewall
    │
    ↓
Server Zone
    │
    ↓
Database Zone
```

Communication between zones can be allowed or blocked according to security rules.

This means that compromising one system does not automatically provide access to everything else.

---

# 2. 🔄 Lateral Movement

**Lateral movement** is when an attacker moves from an initially compromised system to other systems inside a network.

Attackers often do not directly compromise their final target.

Instead, they may follow a path like:

```text
Initial Compromise
        ↓
Compromised Device
        ↓
Network Discovery
        ↓
Credential Theft
        ↓
Lateral Movement
        ↓
Sensitive Systems
        ↓
Valuable Data
```

The first compromised device is often just a **foothold**.

The attacker then tries to move toward more valuable systems.

---

## 🛡️ How Segmentation Helps

Segmentation creates barriers between network zones.

```text
Compromised Device
        ↓
    Current Zone
        ↓
     Firewall
        ↓
Other Zone
        ❌
```

The attacker must overcome additional controls to move further.

This provides:

- Containment
- Reduced lateral movement
- More opportunities for detection
- Reduced attack impact
- Protection for critical systems

---

# 3. 🧱 How Networks Are Segmented

Several technologies can work together to create network segmentation.

---

## 3.1 🔹 Subnets

A **subnet** divides a larger network into smaller IP-based networks.

Example:

```text
Marketing → 192.168.10.x
Finance   → 192.168.20.x
IT        → 192.168.30.x
```

Devices in different subnets generally communicate through a router or Layer 3 device.

This creates a natural point where traffic can be controlled.

### Key idea

> **Subnet = divide a large network into smaller IP networks.**

---

# 3.2 🔹 VLANs

**VLAN** stands for **Virtual Local Area Network**.

VLANs allow multiple logical networks to exist on the same physical network infrastructure.

Example:

```text
                 One Switch
                     │
          ┌──────────┼──────────┐
          ↓          ↓          ↓
       VLAN 10     VLAN 20    VLAN 30
      Marketing    Finance       IT
```

The same physical switch can carry multiple logically separated networks.

### Key idea

> **VLAN = logical network separation on shared physical infrastructure.**

---

# 3.3 🔥 Firewalls Between Zones

Firewalls control which traffic is allowed to cross between network zones.

For example:

```text
Marketing → Internet        ✅ Allowed
Marketing → File Server     ✅ Allowed
Marketing → Payment System  ❌ Blocked
```

A firewall can use a **default-deny** approach.

That means:

> **Block traffic by default and explicitly allow only what is required.**

### Key idea

> **Firewall = controls communication between network zones.**

---

# 3.4 🌐 DMZ

**DMZ** stands for **Demilitarized Zone**.

A DMZ is a separate network zone used for systems that need to be accessible from the Internet.

Examples include:

- Web servers
- Mail servers
- Public-facing applications
- Public APIs

A simplified design:

```text
Internet
    ↓
   DMZ
    ↓
Web Server
    ↓
 Firewall
    ↓
Internal Network
```

If a public-facing server is compromised, segmentation can prevent the attacker from directly reaching the internal network.

### Key idea

> **DMZ = separate zone for public-facing systems.**

---

# 3.5 📶 Guest Networks

A guest network separates visitors or untrusted devices from the main network.

Example:

```text
              Router
             /      \
            /        \
     Main Wi-Fi     Guest Wi-Fi
         │               │
       Laptop        Visitor Phone
```

The guest network can provide Internet access while preventing direct access to important internal devices.

### Key idea

> **Guest Network = isolate visitors and untrusted devices from important systems.**

---

# 4. 📷 IoT Segmentation

**IoT** stands for **Internet of Things**.

Examples include:

- Smart cameras
- Smart TVs
- Smart speakers
- Smart bulbs
- Smart doorbells
- Smart thermostats

IoT devices can sometimes have:

- Weak default credentials
- Outdated software
- Infrequent security updates
- Limited security controls

Because of this, IoT devices should ideally be placed on a separate network.

```text
Main Network
    │
    ├── Laptop
    └── Phone

IoT Network
    │
    ├── Camera
    ├── Smart TV
    └── Smart Speaker
```

The IoT devices can still access the services they need while their ability to reach important devices is restricted.

---

## 🦠 Mirai Botnet

The **Mirai botnet** demonstrated the danger of insecure IoT devices.

Mirai compromised large numbers of poorly secured IoT devices and used them together for large-scale DDoS attacks.

The important lesson is:

> **An insecure device becomes more dangerous when it has unnecessary network access.**

Segmentation can reduce the network reach of such devices.

---

# 5. 🏭 IT and OT Segmentation

**OT** stands for **Operational Technology**.

OT systems control physical processes and machinery.

Examples include:

- Factory equipment
- Power systems
- Water treatment systems
- Industrial control systems

IT and OT networks should be appropriately separated.

```text
Office IT
    ↓
 Firewall
    ↓
   OT Network
    ↓
Industrial Equipment
```

If an employee's office laptop becomes compromised, segmentation can make it harder for an attacker to reach systems controlling physical equipment.

### Key idea

> **IT/OT segmentation helps protect physical systems from threats entering through IT networks.**

---

# 6. 🏪 Small-Business Segmentation Example

A small shop may have:

- 💳 Payment till
- 📷 Security cameras
- 💻 Back-office laptop
- 📱 Customer Wi-Fi

Putting all of them on one flat network creates unnecessary risk.

A better design is:

```text
Payment Zone
    ↓
Payment Till

Camera/IoT Zone
    ↓
Security Cameras

Business Zone
    ↓
Back-office Laptop

Guest Zone
    ↓
Customer Wi-Fi
```

Each zone receives only the network access it actually needs.

---

## 💳 Payment Zone

The payment till should communicate with:

- Required payment-processing services
- Required network services

It should be blocked from:

- Security cameras
- Customer Wi-Fi
- Unnecessary internal systems

```text
Payment Till
     │
     ├── Payment Services → ✅
     ├── Cameras          → ❌
     ├── Customer Wi-Fi  → ❌
     └── Unnecessary LAN → ❌
```

---

## 📷 Camera/IoT Zone

The security cameras should communicate only with the services they require.

They should be blocked from:

- Payment systems
- Back-office laptop
- Customer devices

```text
Cameras
   │
   ├── Required Services → ✅
   ├── Payment Till      → ❌
   ├── Office Laptop     → ❌
   └── Customer Devices  → ❌
```

---

## 💻 Business/Office Zone

The back-office laptop may need access to:

- Business applications
- Business records
- Required services
- Internet

It should not have unnecessary access to:

- Security cameras
- Customer devices
- Other restricted zones

---

## 📱 Guest/Customer Zone

Customer Wi-Fi should provide Internet access only.

```text
Customer Device
      ↓
   Internet
      ↓
      ✅
```

It should be blocked from:

- Payment systems
- Security cameras
- Back-office laptop
- Internal network resources

---

# 7. 🔐 Least Privilege

The principle behind network segmentation is **least privilege**.

Least privilege means:

> **Give something only the access it genuinely needs, and nothing more.**

This principle can apply to users as well as networks.

### User-level least privilege

```text
Employee → Email       ✅
Employee → Payroll DB  ❌
```

### Network-level least privilege

```text
Marketing → Internet        ✅
Marketing → File Server     ✅
Marketing → Payment System  ❌
```

Therefore:

> **Network segmentation is least privilege applied to network connectivity.**

---

# 8. 🚫 Default Deny

**Default deny** means:

> **Block everything by default and explicitly allow only what is required.**

For example:

```text
Traffic Request
      ↓
Is it required?
      ↓
 ┌────┴────┐
Yes       No
 ↓         ↓
Allow     Deny
```

This reduces unnecessary communication paths.

---

# 9. 🛡️ Segmentation and Zero Trust

Segmentation connects to the larger security principle of **Zero Trust**.

Traditional network security can sometimes assume:

> "If something is inside the network, it can be trusted."

Zero Trust challenges that assumption.

The basic idea is:

> **Do not trust automatically. Verify access.**

### Segmentation

```text
Separate the network
        ↓
Control communication
between zones
```

### Zero Trust

```text
Don't trust by default
        ↓
Verify access
        ↓
Give only necessary permissions
```

Zero Trust takes the principle of least privilege further.

---

# 10. 🌐 Real-World Example — Target Breach

The Target breach demonstrates the importance of controlling lateral movement.

Attackers obtained access associated with an **HVAC contractor** and eventually reached Target's payment systems.

An HVAC contractor is a company or service provider that works with **heating, ventilation, and air-conditioning systems**.

A simple lesson from the incident is:

> **Better network segmentation could have made it harder for attackers to move from the HVAC contractor's access to Target's payment systems.**

---

# 11. 🧪 Practical Lab

## Part 1 — Mapping the Network

The first part of the lab involved checking the network that I was connected to.

Because the network I use is managed by someone else, I did **not** access or attempt to access the router's administrative interface.

From my Windows laptop, I checked basic network information using:

```text
ipconfig
```

The laptop showed:

- A private IPv4 address
- A subnet mask
- A default gateway
- A DNS suffix

The network was a normal Wi-Fi connection.

### Important limitation

I could not inspect:

- The router's connected-device list
- VLAN configuration
- Router segmentation settings

Therefore, I could **not conclude that the network was flat**.

The correct conclusion was:

> **The internal segmentation of the network could not be verified because the network infrastructure is managed by someone else.**

---

## Devices Considered

For the exercise, the devices considered were:

- 💻 Laptop
- 📱 Phone

If designing a personal home network, important devices such as a primary laptop and phone could remain on a trusted network while IoT and guest devices could be isolated.

---

# 12. 🧪 Maya's Segmentation Plan

The practical design separated the systems into four zones:

```text
                    INTERNET
                       │
                    Firewall
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
   Payment Zone    Camera/IoT    Business Zone
        │              │              │
       Till          Cameras        Laptop

                       │
                       ↓
                  Guest Zone
                       │
                 Customer Wi-Fi
```

### Final access decisions

| Zone | System | Allowed | Blocked |
|---|---|---|---|
| Payment Zone | Payment Till | Required payment services | Cameras, customer Wi-Fi, unnecessary systems |
| Camera/IoT Zone | Security Cameras | Required camera/network services | Payment till, office laptop, customer devices |
| Business Zone | Back-office Laptop | Business services, required resources, Internet | Cameras, customer Wi-Fi, unnecessary systems |
| Guest Zone | Customer Wi-Fi | Internet | Payment, cameras, office laptop, internal network |

---

# 13. 🔍 Key Observations From the Lab

### Observation 1

A network does not need to be physically separated to be logically segmented.

VLANs can provide logical separation over shared physical infrastructure.

### Observation 2

Segmentation alone is not enough.

Traffic between segments must be controlled using mechanisms such as firewalls and access-control rules.

### Observation 3

Not every device needs to communicate with every other device.

Unnecessary communication creates unnecessary attack paths.

### Observation 4

IoT devices should not automatically be trusted.

They should be separated from more sensitive systems when possible.

### Observation 5

Guest devices should have limited access.

They generally need Internet access, not access to internal systems.

### Observation 6

Segmentation helps contain breaches.

It does not necessarily prevent the initial compromise, but it can limit what happens afterward.

---

# 14. 🧠 Important Connections

The concepts from this lesson connect together:

```text
Initial Compromise
        ↓
Lateral Movement
        ↓
Segmentation
        ↓
Access Controls
        ↓
Containment
        ↓
Reduced Damage
```

And the underlying security principle is:

```text
Least Privilege
       ↓
Allow only necessary access
       ↓
Deny unnecessary access
       ↓
Limit lateral movement
       ↓
Contain the breach
```

---

# 15. 📌 Key Terms

| Term | Simple Meaning |
|---|---|
| **Network Segmentation** | Dividing a network into separate zones |
| **Flat Network** | A network with little separation between devices |
| **Lateral Movement** | Moving from one compromised system to another |
| **Subnet** | A separate IP-based network |
| **VLAN** | Logical network separation on shared infrastructure |
| **Firewall** | Controls traffic between zones |
| **DMZ** | Separate zone for public-facing systems |
| **IoT Network** | Separate network for smart/connected devices |
| **Guest Network** | Isolated network for visitors |
| **Least Privilege** | Give only the access that is necessary |
| **Default Deny** | Block by default and allow only what is required |
| **Zero Trust** | Do not automatically trust; verify access |
| **OT** | Technology used to monitor/control physical processes |

---

# 🎯 Final Takeaway

The most important lesson from Day 34 is:

> **Don't allow everything to communicate with everything.**

Instead:

```text
Separate
   ↓
Allow only what is needed
   ↓
Block unnecessary access
   ↓
Limit lateral movement
   ↓
Contain breaches
```

Network segmentation turns:

> **"An attacker got into one device."**

into a situation where:

> **"The attacker is contained and cannot freely reach everything else."**

The goal is not to make breaches impossible.

The goal is to make sure:

> **One breach does not become total loss.**

---

## 📚 Day 34 Summary

**Topic:** Network Segmentation

**Main concept:** Divide a network into zones and control communication between them.

**Main threat addressed:** Lateral movement.

**Security principle:** Least privilege.

**Important technologies:** Subnets, VLANs, firewalls, DMZs, guest networks, and IoT networks.

**Main defensive goal:** Containment.

**Practical work:** Mapped the network information available from my connection and designed a segmentation plan based on least privilege and necessary communication.

**One-line lesson:**

> **Segment the network, restrict unnecessary communication, and make sure one compromised device cannot become a compromise of everything.**