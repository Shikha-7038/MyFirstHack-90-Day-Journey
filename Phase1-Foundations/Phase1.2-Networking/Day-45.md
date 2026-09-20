# 🔐 Day 45 — Networks Capstone: Network Defense Plan

**MyFirstHack 90-Day Cybersecurity Journey**  
**Phase:** Networks  
**Day:** 45  
**Task:** Design a Network Defense Plan for a Small Business

---

## 🎯 Objective

The goal of today's capstone was to apply the networking and cybersecurity concepts learned throughout the Networks phase to a realistic small-business scenario.

Instead of analysing one individual security concept, I had to look at the **entire network**, identify assets and weaknesses, think about how an attacker could potentially move through the environment, prioritise risks, design practical defenses, and determine how those controls could be verified and monitored.

The overall workflow was:

**Discover → Assess → Prioritise → Think Like an Attacker → Defend → Verify → Monitor → Respond → Improve**

---

# 🏪 1. Scenario — Maya's Clothing Shop

Maya runs a small clothing shop that has grown organically over time.

The shop uses several different types of devices, but they have all been connected to the same network without proper segmentation.

### Network environment

- 2 payment tills
- 4 security cameras
- Back-office laptop containing business records and customer details
- Maya's personal laptop used for business and personal browsing
- 2 staff phones
- Smart speaker
- Network printer
- Customer Wi-Fi
- ISP-provided router

### Existing security concerns

- All devices are on one **flat network**
- Customer Wi-Fi shares the same network as the payment systems
- Wi-Fi password has not changed for 3 years
- Wi-Fi password is written on a chalkboard
- Router still uses its default admin credentials
- Security cameras have never been updated
- No monitoring or regular log review is in place
- Staff sometimes use the back-office laptop containing customer information
- It is unclear whether the router firewall is properly configured

---

# 🔎 2. Step One — Identify and Understand the Assets

Before identifying vulnerabilities, I first needed to understand **what exists on the network and what each device does**.

I categorised the devices according to their role and importance.

| Asset | Category | Purpose | Potential Impact |
|---|---|---|---|
| Payment Till 1 | Payment | Card payments | Financial loss, disruption, compliance concerns |
| Payment Till 2 | Payment | Card payments | Financial loss, disruption |
| 4 Security Cameras | IoT | Security monitoring | Loss of surveillance, privacy concerns |
| Back-office Laptop | Data | Business/customer information | Data exposure, privacy/legal consequences |
| Maya's Laptop | Personal | Business + personal use | Data exposure, business disruption |
| Staff Phones | Staff | Communication/Wi-Fi | Network exposure |
| Smart Speaker | IoT | Smart assistant | Privacy/network risk |
| Network Printer | Infrastructure | Business printing | Document exposure/disruption |
| Customer Wi-Fi | Guest | Internet access | Untrusted network access |
| Router | Infrastructure | Internet/network connectivity | Loss of network control |

### Key observation

The most important assets were:

1. **Payment systems**
2. **Back-office laptop**
3. **Router/network infrastructure**

This showed me that asset identification is not simply about counting devices. It is about understanding **what each device protects or enables**.

---

# ⚠️ 3. Step Two — Identify the Risks

After understanding the environment, I looked at what could go wrong.

### Risk 1 — Flat Network

All devices were connected to the same network.

If one device were compromised, there would be fewer network boundaries to prevent communication with other systems.

**Potential consequence:**  
Lateral movement toward more valuable systems.

---

### Risk 2 — Customer Wi-Fi Shares the Payment Network

Customer devices are untrusted.

Allowing them to exist on the same network as payment systems creates an unnecessary security risk.

**Potential consequence:**

- Increased exposure of payment systems
- Business disruption
- Wider incident impact
- Payment-security/compliance concerns

---

### Risk 3 — Default Router Credentials

The router's administrator credentials had never been changed from the default.

If an attacker obtained management access, they could potentially change network settings.

**Potential consequence:**

- Loss of network control
- Traffic manipulation
- Business disruption

---

### Risk 4 — Old and Exposed Wi-Fi Password

The Wi-Fi password had remained unchanged for 3 years and was physically written on a chalkboard.

This increases the possibility of unauthorised people knowing the credentials.

---

### Risk 5 — Outdated Cameras

The security cameras had never been updated since installation.

Unpatched devices may contain vulnerabilities that remain unresolved.

They also represent additional IoT attack surface.

---

### Risk 6 — No Monitoring or Log Review

There was no established process for monitoring the network or reviewing logs.

This means suspicious activity could potentially remain unnoticed.

It would also make investigating an incident more difficult because there may be limited evidence available.

---

### Risk 7 — Sensitive Data on a Shared Back-office Laptop

The back-office laptop contains business records and customer information, while staff may use it for general activities.

Unnecessary access or unsafe activity could increase the chance of data exposure or compromise.

---

# 🎯 4. Step Three — Prioritise the Risks

Not every security weakness has the same importance.

I used **likelihood and impact** to determine which risks should receive attention first.

### Risk priority concept

**Risk Priority ≈ Likelihood × Impact**

### 🔴 Critical

- Flat network
- Customer Wi-Fi sharing the environment with payment systems
- Default router credentials

### 🟠 High

- Exposed/old Wi-Fi password
- No monitoring or log review

### 🟡 Medium

- Never-updated cameras
- Back-office laptop containing customer information
- Maya's dual-use laptop
- Staff devices and printer creating additional attack surface

### 🟢 Low

- Smart speaker and its immediate impact

### Key lesson

A weakness becomes more important when it can realistically affect a **high-value asset**.

For example:

A compromised smart speaker may have limited immediate business impact.

A compromise involving a payment system could cause much greater financial and operational consequences.

---

# 🧭 5. Step Four — Think Like an Attacker

I then considered a **plausible attack path**.

This was a risk scenario, not evidence that an attack had actually occurred.

### Example path

**Unauthorised User / Attacker**

↓  

**Customer Wi-Fi**

Old password + password physically exposed

↓

**Flat Network**

No segmentation

↓

**Internal Devices**

Payment tills • laptops • cameras • printer • IoT

↓

**High-Value Targets**

Payment systems • Back-office laptop • Router

### Why this path is concerning

The important issue was not simply that the Wi-Fi password was old.

The bigger problem was the combination of:

**Old/exposed credentials + untrusted customer devices + flat network + valuable internal systems + limited monitoring**

This created the possibility of a large **blast radius** if a low-trust device were compromised.

---

# 🛡️ 6. Step Five — Design the Defense

The most important recommendation was **network segmentation**.

Instead of allowing every device to communicate within one flat network, I redesigned the environment into separate security zones.

### Proposed structure

**Internet**

↓

**Router + Firewall**

↓

**Network Segmentation**

### 💳 Payment Zone

Contains:

- Payment Till 1
- Payment Till 2

Only required payment communication should be permitted.

---

### 💻 Business Zone

Contains:

- Back-office laptop
- Approved business devices

Access should be restricted to authorised users and necessary resources.

---

### 📱 Staff Zone

Contains:

- Staff phones
- Approved business devices

Access should be limited according to business requirements.

---

### 📷 IoT Zone

Contains:

- Security cameras
- Smart speaker
- Network printer

IoT devices should be isolated from critical systems wherever possible.

---

### 👥 Guest Zone

Contains:

- Customer Wi-Fi
- Customer devices

Customers should receive internet access without being able to reach payment or business networks.

---

# 🔐 7. Additional Security Controls

Segmentation alone is not enough.

I also recommended:

### Router Security

- Change default administrator credentials
- Disable remote administration unless required
- Update router firmware
- Check and configure the firewall

### Wi-Fi Security

- Use a strong unique password
- Use WPA3 if supported, otherwise strong WPA2
- Remove the password from the public chalkboard
- Separate customer Wi-Fi from business networks

### Device Security

- Update supported cameras
- Replace unsupported devices
- Keep laptops patched
- Restrict access to sensitive business information

### Monitoring

- Enable useful logging
- Monitor important security events
- Establish a basic log-review process
- Investigate suspicious activity

### Recovery

- Maintain backups of important business information
- Have a basic incident-response process
- Test whether security controls continue to work

---

# ✅ 8. Step Six — Verify the Controls

A security control should not simply be configured and assumed to work.

It should be **tested**.

### Example verification

**Customer Wi-Fi → Internet**

✅ Allowed

**Customer Wi-Fi → Payment Network**

❌ Blocked

**Customer Wi-Fi → Business Network**

❌ Blocked

**Customer Wi-Fi → Router Management**

❌ Blocked

**IoT → Payment Network**

❌ Blocked

### Other verification checks

- Default router password no longer works
- Firewall is enabled/configured
- Business Wi-Fi uses appropriate security
- Cameras are updated or replaced
- IoT devices are isolated
- Important security events are being logged
- Logs are actually reviewed

### Key lesson

**Having a control is not the same as proving that the control works.**

---

# 📊 9. Step Seven — Monitor the Environment

Even a strong defense cannot guarantee that an attack will never happen.

Monitoring provides visibility.

Important sources include:

- Network traffic
- Firewall events
- Authentication events
- System/device logs
- IDS/IPS alerts
- SIEM events

### Example

**Customer device**

↓

Attempts to communicate with payment network

↓

**Firewall blocks connection**

↓

**Event is logged**

↓

**Alert is reviewed**

↓

**Analyst investigates**

This connects several concepts I learned during the Networks phase:

**Logs → SIEM → IDS/IPS → Network Traffic → Alerts → Investigation**

---

# 🚨 10. Step Eight — Respond to Suspicious Activity

If monitoring produces a suspicious alert, the analyst should not immediately assume that it is malicious.

The response should be evidence-based.

### Response workflow

**Validate**

Determine what happened and whether the activity is expected.

↓

**Contain**

Isolate the affected device or connection if necessary.

↓

**Investigate**

Review logs, network traffic, authentication events, IDS/IPS alerts, and other available evidence.

↓

**Recover**

Restore affected systems safely and remediate the issue.

↓

**Improve**

Use the lessons learned to strengthen the defense.

### SOC thinking

The process is not simply:

**Alert → Block**

It is:

**Alert → Validate → Investigate → Contain → Respond → Document**

---

# 🔄 11. Recover and Improve

After an incident, the goal is not just to return to normal.

The organization should ask:

- What happened?
- Why did it happen?
- What controls worked?
- What failed?
- Did we have enough evidence?
- How can we reduce the chance of recurrence?

For example, if a customer device was able to reach an internal system, the long-term solution should address the **root cause**, not only the individual device.

That could mean improving:

- Network segmentation
- Firewall rules
- Access controls
- Monitoring
- Patch management
- Security policies
- Incident-response procedures

---

# 📋 12. Final Action Plan

## 🔴 Do First

- Implement network segmentation
- Isolate customer Wi-Fi
- Separate payment systems
- Change router administrator credentials
- Check/enable firewall
- Change the business Wi-Fi password
- Remove the password from the chalkboard

## 🟠 This Week

- Update or replace cameras
- Isolate IoT devices
- Secure the back-office laptop
- Review staff-device access
- Configure basic monitoring and logging
- Secure the printer

## 🟢 This Month

- Review accounts and access permissions
- Remove unnecessary devices/accounts
- Test network segmentation
- Review firewall configuration
- Establish an incident-response process
- Schedule regular security reviews

---

# 🔍 13. Verification Criteria

The defense plan should be considered successful when:

- Customer Wi-Fi can access the internet but cannot reach payment/business systems
- Payment systems are isolated from unnecessary devices
- Default router credentials have been replaced
- Firewall protection is verified
- Business Wi-Fi is securely configured
- IoT devices are isolated and updated
- Sensitive data has appropriate access restrictions
- Important security events are logged
- Logs are reviewed regularly
- Security controls are tested after implementation

---

# 🧠 14. SOC Analyst Connection

This capstone helped me understand that defensive security is much broader than simply watching alerts.

A security analyst needs to understand:

**What is connected?**  
↓  
**What is important?**  
↓  
**What could go wrong?**  
↓  
**How could an attacker move?**  
↓  
**Which risks matter most?**  
↓  
**How can we reduce them?**  
↓  
**Can we prove the controls work?**  
↓  
**How will we detect suspicious activity?**  
↓  
**How will we respond?**

This connects the technical side of cybersecurity with **risk assessment, business impact, communication, and decision-making**.

---

# 💡 15. Key Learnings

### 1. A network is more than connectivity

A network also defines **trust boundaries, access, and communication paths**.

### 2. Segmentation limits blast radius

If everything is connected, one compromised device can potentially create a much larger problem.

### 3. Not every vulnerability deserves equal priority

Security decisions should consider both **likelihood and impact**.

### 4. Prevention and detection work together

Firewalls and segmentation can restrict unwanted communication, while logs and monitoring provide visibility into what is happening.

### 5. Verification matters

A security control should be tested rather than simply assumed to work.

### 6. Security recommendations should be practical

A good defense plan should tell the business:

**What should be fixed? → Why? → How urgent is it? → How can we verify it?**

---

# 🔎 → 📊 → 🛡️ 16. Networks Phase Progression

Looking back at this phase, I can see a clear progression:

### FIND
**Network Footprint Report**

Understand what exists on the network.

↓

### ANALYSE
**Traffic Investigation Report**

Investigate what is happening and identify suspicious behavior.

↓

### DEFEND
**Network Defense Plan**

Use the information gathered to design practical defenses.

This helped me see how individual networking and security concepts fit into a larger defensive workflow.

---

# 🎯 Final Reflection

Today's capstone brought together many of the concepts I learned throughout the Networks phase, including:

- Networking fundamentals
- Wireshark and packet analysis
- Network attacks
- NAT
- VPNs
- Proxies
- IPv6
- Wireless security
- DNS tunneling
- IDS/IPS
- SIEM
- Logs
- Network forensics
- Zero Trust
- Network segmentation

The biggest shift for me was moving from **learning individual concepts** to thinking about how those concepts work together in a real security scenario.

The key lesson I am taking forward is:

> **A network is not just about connecting devices. It's also about controlling trust, limiting access, and containing damage.**

### Overall workflow

**Discover → Assess → Prioritise → Think Like an Attacker → Defend → Verify → Monitor → Respond → Improve**

**45 days completed. Still learning. Still building. 🚀**