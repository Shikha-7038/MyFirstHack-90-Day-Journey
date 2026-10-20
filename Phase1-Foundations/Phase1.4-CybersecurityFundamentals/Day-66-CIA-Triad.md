# Day 66 — CIA Triad

## Task

The task was to understand the **CIA Triad** and apply its three security properties — **Confidentiality, Integrity, and Availability** — to common cybersecurity situations.

The goal was to understand what security is protecting, how attacks can affect these properties, and how security decisions involve balancing protection with usability and context.

---

## 1. Confidentiality

**Confidentiality** means making sure information is only accessible to the people or systems that are authorised to see it.

**Key question:** Who is allowed to see it?

### Examples

- Access-controlled medical records
- Encrypted messages
- Private cloud storage
- Role-based access controls

### When confidentiality fails

- An unauthorised person views private records.
- Private information is exposed or disclosed without permission.

---

## 2. Integrity

**Integrity** means making sure information remains accurate, trustworthy, and protected from unauthorised changes.

**Key question:** Can the information be trusted?

### Examples

- Hash verification of downloaded files
- Database change controls
- Digital signatures
- File integrity monitoring

### When integrity fails

- Software is modified without authorisation.
- A stored record is changed incorrectly or maliciously.

---

## 3. Availability

**Availability** means making sure authorised users can access systems and information when they need them.

**Key question:** Can authorised users access it?

### Examples

- Regular data backups
- Redundant servers
- Disaster recovery systems
- System monitoring

### When availability fails

- A critical service becomes unavailable.
- Users cannot access required systems or information.

---

## 4. Applying the CIA Triad to Security Controls

The CIA Triad can be used to understand the purpose of security controls learned throughout the journey.

| Security Control / Practice | CIA Property | How it helps |
|---|---|---|
| File permissions | Confidentiality + Integrity | Controls who can access or modify files. |
| SSH | Confidentiality + Integrity | Protects remote communication from exposure or alteration. |
| Passwords and MFA | Confidentiality | Helps prevent unauthorised access. |
| Firewalls and network segmentation | Confidentiality + Integrity + Availability | Controls network access, limits unauthorised communication, and can reduce attack impact. |
| Software updates | Confidentiality + Integrity + Availability | Fix vulnerabilities that could allow attackers to access, modify, or disrupt systems. |

---

## 5. Attack → CIA Mapping

| Attack / Incident | CIA Property Affected |
|---|---|
| Stolen customer database | Confidentiality |
| Ransomware encrypting company files | Availability + Integrity |
| Attacker tampering with bank transaction records | Integrity |
| Eavesdropping on an unencrypted network connection | Confidentiality |
| Denial-of-service attack | Availability |

---

## 6. Security and Convenience Trade-Off

Security controls can improve protection while adding some inconvenience for users.

### Example: Multi-Factor Authentication (MFA)

- **Security gained:** Adds another verification step and reduces the risk of unauthorised access.
- **Convenience reduced:** Users must complete an additional authentication step when logging in.

This shows that security is not simply about adding as many controls as possible. Security decisions should balance protection with usability and the needs of the environment.

---

## 7. Context Changes Security Priorities

The most important CIA property can change depending on the system and the consequences of failure.

| Scenario | Most Important Property | Reason |
|---|---|---|
| Hospital life-support monitoring | Availability | Continuous access can directly affect patient care. |
| Journalist's confidential source files | Confidentiality | Unauthorised disclosure could expose sensitive sources. |
| Online bank account balances | Integrity | Financial records must remain accurate and trustworthy. |
| E-commerce payment system | Integrity | Prices, orders, and payment records must remain accurate. |
| Railway signalling system | Availability | The system needs to remain operational when required. |
| Unpublished research | Confidentiality | Sensitive research information should not be disclosed without authorisation. |

No single CIA property is always the most important. The appropriate balance depends on the system, its users, and the consequences of a security failure.

---

## 8. Security Trade-Off Example

### Automatic Screen Lock

**Security gained:**
- Protects information when a device is left unattended.

**Convenience reduced:**
- The user must unlock the device again after inactivity.

This is an example of balancing security protection with user convenience.

---

## 9. Task Application

### Step 1 — Define the CIA Triad

- **Confidentiality:** Making sure information is only accessible to the people or systems that are authorised to see it.
- **Integrity:** Making sure information remains accurate, trustworthy, and protected from unauthorised changes.
- **Availability:** Making sure authorised users can access systems and information when they need them.

### Step 2 — Memory Questions

- **Confidentiality →** Who can see it?
- **Integrity →** Can I trust it?
- **Availability →** Can I access it?

### Step 3 — Connect Previous Learning to CIA

- File permissions → Confidentiality + Integrity
- SSH → Confidentiality + Integrity
- Passwords and MFA → Confidentiality
- Firewalls and network segmentation → All three CIA properties
- Software updates → All three CIA properties

### Step 4 — Classify Security Incidents

- Stolen customer database → Confidentiality
- Ransomware encrypting files → Availability + Integrity
- Bank transaction tampering → Integrity
- Eavesdropping on unencrypted traffic → Confidentiality
- Denial-of-service attack → Availability

### Step 5 — Consider Security Trade-Offs

MFA was used as an example of a security control that improves protection but adds an extra step for users. This demonstrates the need to balance security with convenience.

### Step 6 — Consider Context

Different systems have different priorities:

- Hospital life-support monitoring → Availability
- Journalist's confidential source files → Confidentiality
- Online bank account balances → Integrity

The consequences of a security failure determine which property needs greater protection.

---

## Key Takeaways

- The **CIA Triad** consists of Confidentiality, Integrity, and Availability.
- **Confidentiality** protects information from unauthorised access or disclosure.
- **Integrity** protects information from unauthorised modification and helps keep it accurate and trustworthy.
- **Availability** keeps systems and information accessible to authorised users when needed.
- Security controls can protect one or more CIA properties at the same time.
- Attacks can be classified by which CIA property they affect.
- Ransomware can affect both availability and integrity by making data inaccessible and altering its state through encryption.
- Security is not only about adding controls; controls can introduce usability and convenience trade-offs.
- The importance of confidentiality, integrity, and availability depends on the system and the consequences of failure.
- The CIA Triad provides a common way to discuss what security is protecting and what could happen when protection fails.
- A useful starting point for analysing a security problem is: **What am I protecting, and what happens if it is exposed, changed, or unavailable?**
