# Day 44 — SOC Analyst: From the First Alert

## 🎯 Objective

Today's lesson focused on understanding the **Security Operations Center (SOC)** and the role of a **SOC Analyst**.

Instead of learning another individual security tool, I focused on understanding how the skills from previous days come together in a real cybersecurity workflow.

The main goal was to understand how a SOC Analyst receives an alert, evaluates it, investigates suspicious activity, documents findings, and escalates genuine threats.

---

## 🛡️ What is a SOC?

**SOC** stands for **Security Operations Center**.

A SOC is a team or function responsible for continuously monitoring an organization's security, investigating suspicious activity, and helping detect and respond to threats.

A SOC may monitor:

- Security alerts
- Network traffic
- Authentication activity
- Endpoint activity
- Firewall events
- IDS/IPS alerts
- SIEM events
- DNS activity
- Other security logs

A SOC does not necessarily have to be a physical room. It can be a distributed team working across different locations and shifts.

Because security monitoring can be continuous, some SOCs operate **24/7**.

---

## 👩‍💻 What Does a SOC Analyst Do?

A SOC Analyst monitors security events and determines whether they represent normal activity, suspicious behavior, or a potential security incident.

A simplified SOC workflow is:

**🚨 Alert → 🧠 Triage → 🔎 Investigate → 📝 Document → 🛡️ Escalate/Respond → 🤝 Handover**

The important point is that an **alert is only the starting point**.

The analyst has to understand:

- What happened?
- Why did the alert trigger?
- Is the activity normal?
- Is it suspicious?
- What evidence supports the conclusion?
- What should happen next?

---

## 🧠 What is Alert Triage?

**Triage** is the process of quickly assessing an alert to determine its importance and decide what action should be taken.

A SOC Analyst may classify activity as:

🟢 **Routine / Benign**  
Normal activity or something with little evidence of a security incident.

🟡 **False Positive**  
The security system generated an alert, but investigation shows that it was not actually a security incident.

🔴 **Potentially Serious**  
Activity that requires further investigation because it may indicate malicious behavior or compromise.

The objective is not to investigate every alert with the same level of urgency.

The analyst needs to identify which alerts deserve attention first.

---

## ⚠️ False Positives

Not every alert represents an attack.

For example, an **impossible-travel alert** may show a user logging in from London and then Paris only 20 minutes later.

This could indicate:

- Stolen credentials
- Account compromise

But it could also have a legitimate explanation:

- The user is travelling
- The user is connected through a VPN
- The VPN server is located in another country

The analyst should therefore investigate the evidence instead of immediately declaring it an attack.

Useful evidence includes:

- Authentication logs
- Source IP address
- Device information
- Session information
- VPN usage
- Previous login activity

This demonstrates an important SOC skill:

**Don't react to the alert alone. Investigate the context behind it.**

---

# 🏢 SOC Tiers

SOC teams commonly use different levels of responsibility.

## Tier 1 — Initial Triage

Tier 1 analysts are often responsible for:

- Reviewing alerts
- Performing initial triage
- Identifying false positives
- Conducting basic investigation
- Collecting initial evidence
- Escalating suspicious cases

This can be a common entry point into defensive cybersecurity.

---

## Tier 2 — Deeper Investigation

Tier 2 analysts perform more detailed investigations.

Responsibilities can include:

- Incident analysis
- Correlating multiple events
- Investigating affected systems
- Determining the scope of an incident
- Supporting containment and response

---

## Tier 3 — Advanced Investigation

Tier 3 analysts handle more complex security situations.

Their responsibilities may include:

- Advanced incident response
- Threat hunting
- Complex investigations
- Malware or attacker behavior analysis
- Developing detection improvements

The exact responsibilities of each tier can vary between organizations.

---

# 🔎 Example: Possible DNS Tunneling

One of the alerts reviewed during today's task involved unusual DNS traffic.

The alert showed:

- Hundreds of DNS queries per minute
- Long, random-looking subdomains
- One unfamiliar domain

This pattern could indicate **DNS tunneling**.

Since I had previously learned about DNS tunneling, I could connect today's alert to Day 43.

For investigation, I would examine:

- DNS logs
- SIEM events
- Packet captures
- Source device
- User associated with the device
- Domain information
- Timeline of activity
- Other related suspicious events

The important lesson is that a SOC Analyst does not simply see an alert saying "DNS tunneling" and immediately assume compromise.

The analyst gathers evidence and determines whether the behavior is actually suspicious.

---

# 🌐 Example: Internal Network Scanning

Another serious alert involved an internal workstation rapidly scanning many other internal machines.

This could indicate:

- Network reconnaissance
- Discovery activity
- A compromised workstation
- An unauthorized security scan

I would investigate:

- Network/IDS logs
- SIEM events
- Packet captures
- Source workstation
- Destination systems
- Timing and frequency
- Other suspicious activity from the same device

If a workstation that normally performs ordinary business activity suddenly begins scanning many internal systems, the behavior becomes more suspicious.

---

# 📝 Documentation

Documentation is an important part of SOC work.

An investigation should record things such as:

- What happened
- When it happened
- Which system or user was affected
- What evidence was found
- Why the activity was considered suspicious
- What actions were taken
- What needs to happen next

Good documentation allows another analyst to understand the investigation without repeating all the previous work.

---

# 🤝 Shift Handover

SOC operations can continue across multiple analysts and shifts.

At the end of a shift, an analyst needs to communicate:

- Open investigations
- Important findings
- Evidence collected
- Actions already taken
- Recommended next steps
- Things the next analyst should continue monitoring

A good handover is like **passing a baton**.

The next analyst should be able to continue the investigation rather than starting from the beginning.

---

# 🚨 Alert Fatigue

SOC analysts may receive a large number of alerts.

If too many unnecessary or repetitive alerts are generated, analysts can experience **alert fatigue**.

This can make it harder to notice genuinely important threats.

This is why SOC teams may:

- Tune detection rules
- Reduce unnecessary alerts
- Improve correlation logic
- Review false positives
- Prioritize alerts based on risk

This connects directly with the SIEM and IDS/IPS concepts I learned previously.

---

# 🧩 How My Previous Learning Connects

Today's lesson helped me see how the topics from previous days fit into an actual security workflow.

### 🌐 Networking
Understanding IP, TCP/UDP, DNS, ARP, NAT, VPNs, and proxies helps an analyst understand network behavior.

### 🔎 Traffic Analysis
Packet captures and Wireshark can provide network-level evidence.

### ⚔️ Attacks
Understanding attack techniques helps identify suspicious behavior.

### 🛡️ IDS/IPS
These systems can detect suspicious network activity and generate alerts.

### 📊 SIEM
A SIEM can collect and correlate security events from different sources.

### 📋 Logs
Logs provide evidence about what happened, when it happened, and which systems or users were involved.

### 🕐 Timelines
A timeline helps reconstruct the sequence of events during an investigation.

### 🔍 Investigation
Multiple pieces of evidence can be connected to understand what actually happened.

### 📝 Documentation
Clear documentation allows other analysts to understand and continue an investigation.

### 🛡️ SOC
The SOC brings these skills together into a continuous security-monitoring and response process.

---

# 🧪 Task Completed

During today's practical task, I reviewed six security alerts and classified them based on their risk.

### Alert 1
**Three failed logins followed by a successful login from the usual office**

**Classification:** 🟢 Routine

The activity could be explained by a user entering the wrong password several times.

---

### Alert 2
**Hundreds of DNS queries per minute using long, random-looking subdomains**

**Classification:** 🔴 Serious

The behavior could indicate DNS tunneling and required further investigation.

---

### Alert 3
**Impossible travel from London to Paris within 20 minutes**

**Classification:** 🔴 Serious for triage

The activity could indicate stolen credentials, but VPN usage could provide a legitimate explanation.

---

### Alert 4
**Single antivirus detection that was automatically quarantined and identified as known adware**

**Classification:** 🟢 Routine

The threat was known and had already been contained.

---

### Alert 5
**Internal workstation rapidly scanning many internal machines**

**Classification:** 🔴 Serious

The behavior could indicate reconnaissance or a compromised system.

---

### Alert 6
**One inbound connection blocked by the firewall**

**Classification:** 🟢 Routine

A single blocked attempt does not provide strong evidence of a successful compromise.

---

## 🔎 Most Serious Alerts

The two alerts I considered most serious were:

### 1. Possible DNS Tunneling

The combination of:

**High DNS volume + long random-looking subdomains + unfamiliar domain**

made this activity worth investigating.

### 2. Internal Network Scanning

A workstation rapidly scanning many internal systems could indicate reconnaissance or compromise.

These alerts demonstrated why understanding normal network behavior is important.

---

# 📋 Handover Summary

At the end of the task, I created a handover summary:

> During the shift, Alerts 1, 4, and 6 were closed as routine because they showed limited or contained activity with no strong evidence of compromise.
>
> Alerts 2 and 5 were escalated for further investigation. Alert 2 showed unusually high-volume DNS traffic with long, random-looking subdomains going to one unfamiliar domain, which could indicate DNS tunneling. Alert 5 involved an internal workstation rapidly scanning many other internal machines, which could indicate reconnaissance or a compromised system.
>
> Alert 3, the impossible-travel login, also requires investigation because the London-to-Paris activity could have either a legitimate VPN explanation or indicate stolen credentials. The next analyst should review authentication logs, source IPs, device/session information, and continue monitoring Alerts 2 and 5 for related activity.

---

# 💡 Key Takeaways

### 1. An alert is only the beginning.

A SOC Analyst needs to investigate the context and evidence behind an alert.

### 2. Not every alert is an attack.

False positives are a normal part of security monitoring.

### 3. Triage requires judgement.

The analyst needs to decide which events are routine and which require deeper investigation.

### 4. Evidence matters.

Logs, packet captures, SIEM events, authentication data, and timelines help support an investigation.

### 5. Documentation matters.

A good investigation is not complete if the findings cannot be clearly communicated to another analyst.

### 6. SOC work is team-based.

Handover and escalation allow investigations to continue across analysts and shifts.

### 7. Technical skills work together.

Networking, attacks, defensive tools, logs, investigation, and documentation are not isolated skills.

---

# 🧭 SOC and the Cybersecurity Career

I also learned that there isn't just one way into cybersecurity.

People can enter through different routes such as:

- Education
- Hands-on learning
- IT or networking experience
- Internships
- Entry-level security roles
- Certifications
- Portfolio projects

Certifications can help demonstrate knowledge, while hands-on work and a portfolio can demonstrate practical ability.

SOC is **one common entry point into defensive cybersecurity**, but it is not the entire cybersecurity field.

Experience in SOC can lead toward areas such as:

- Incident Response & DFIR
- Threat Hunting
- Security Engineering
- Penetration Testing
- Cloud Security
- Application Security
- Identity and Access Management (IAM)
- Governance, Risk & Compliance (GRC)

At the same time, people can enter these areas through other routes without starting in a SOC.

---

# 🧠 Final Reflection

Today's lesson changed my understanding of what a SOC Analyst actually does.

I initially associated cybersecurity operations with detecting attacks and responding to threats. Today I learned that much of the work involves **methodical analysis and decision-making**.

A SOC Analyst needs to recognize patterns, understand what normal activity looks like, investigate suspicious behavior, separate false positives from genuine threats, document evidence, and communicate findings clearly.

The biggest lesson from Day 44 is:

> **The tools can generate the alert. The analyst has to understand what it means.**

This connected many of the topics I have learned throughout the journey into one practical workflow:

**Networking → Attacks → Defensive Tools → Logs → Investigation → Documentation → SOC**

Day 44 helped me understand not only the technology, but also **where those skills fit into an actual cybersecurity role.**