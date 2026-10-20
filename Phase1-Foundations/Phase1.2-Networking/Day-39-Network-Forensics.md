# Day 39 — Network Forensics

**90 Days of Cybersecurity Journey with MyFirstHack**  
**Topic:** Network Forensics  
**Day:** 39 of 90

---

## 1. Introduction

Today I learned about **Network Forensics**, the process of investigating a cyber incident by analysing the evidence left behind across a network.

Every cyber incident eventually leads to an important question:

> **What exactly happened?**

Network forensics helps answer this question by collecting and analysing evidence such as **logs, packet captures, and security alerts**. The goal is to reconstruct the incident and create a clear timeline showing how the attack happened.

Unlike real-time detection, which focuses on identifying suspicious activity as it occurs, network forensics focuses on understanding the complete incident by examining the available evidence.

---

## 2. What I Learned

Network forensics brings together several topics I have learned during the Networks track, including:

- Packet captures and Wireshark
- Reading network traffic
- Recognising network attacks
- Traffic investigation
- IDS and IPS
- SIEM
- Logs

These different sources of information can be combined to reconstruct the complete story of a cyber incident.

The main evidence used during an investigation can include:

- Authentication logs
- Network logs
- System logs
- Application logs
- Packet captures
- IDS/IPS alerts
- SIEM events

---

# 3. Building an Incident Timeline

The central output of a forensic investigation is an **incident timeline**.

A timeline places events collected from different systems into chronological order. This helps investigators turn scattered evidence into an understandable story.

For example:

> **Initial Access → Internal Reconnaissance → Data Access → Data Exfiltration**

Different sources provide different pieces of the investigation:

- **Authentication logs** show when and how an account was accessed.
- **Network logs and packet captures** show communications between systems.
- **System logs** can show activity on compromised devices.
- **Application and database logs** can show what information was accessed.
- **IDS/IPS and SIEM alerts** can identify suspicious activity.

When these events are placed in the correct time order, they can reveal how an attacker moved through an environment.

---

# 4. The Main Questions Network Forensics Answers

A forensic investigation is structured around several important questions.

## How did they get in?

This is known as **Initial Access**.

Investigators try to identify how the attacker entered the environment.

Possible methods include:

- Phishing
- Stolen credentials
- Exploited vulnerabilities
- Compromised third parties
- Stolen devices

Finding the entry point is important because the organisation must fix the weakness that allowed the attacker to enter.

---

## What did they do once inside?

Investigators examine the attacker's actions after gaining access.

They may investigate:

- Systems accessed
- Commands or programs executed
- Privilege escalation
- Internal reconnaissance
- Lateral movement

**Lateral movement** occurs when an attacker moves from one system to another inside a network.

---

## What did they access or take?

This question helps determine the **impact of the incident**.

Investigators try to identify:

- Data accessed
- Files copied
- Sensitive information exposed
- Data transferred outside the organisation

Understanding the impact is important for incident response and possible legal or regulatory obligations.

---

## Are they still inside?

This relates to **Persistence**.

Attackers may establish methods to maintain access, including:

- Backdoors
- New accounts
- Scheduled tasks
- Malicious services
- Additional stolen credentials

A thorough investigation must determine whether the attacker still has a way to access the environment.

---

## When did everything happen?

This is answered through the forensic timeline.

The timeline establishes:

- The sequence of events
- The attacker's actions
- The order in which systems were accessed
- How long the attacker remained undetected

This duration is known as **dwell time**.

---

# 5. Why Synchronised Clocks Are Important

Forensic investigations often combine evidence from multiple systems.

For example:

- Mail servers
- Authentication systems
- Firewalls
- Databases
- IDS/IPS
- SIEM platforms

If these systems have incorrect or unsynchronised clocks, events may appear in the wrong order.

This can result in an inaccurate investigation.

Therefore:

> **Accurate and synchronised timestamps are essential for building a reliable forensic timeline.**

Time synchronisation technologies such as **NTP (Network Time Protocol)** help systems maintain consistent timestamps.

---

# 6. Evidence Handling

Digital forensic evidence must be handled carefully because it may later be required for:

- Legal proceedings
- Lawsuits
- Insurance investigations
- Regulatory investigations

Forensics requires more than simply finding evidence. Investigators must also ensure that the evidence remains reliable and trustworthy.

---

## Preserve the Original Evidence

A core forensic principle is:

> **Preserve the original evidence and work on copies.**

The original evidence should not be directly analysed if doing so could modify it.

Instead, investigators:

1. Preserve the original evidence.
2. Create an exact copy.
3. Verify the copy.
4. Perform analysis on the verified copy.

For network forensics, evidence may include:

- Packet capture files
- Network logs
- Firewall logs
- Authentication logs
- Security alerts

---

# 7. Cryptographic Hashes

A **cryptographic hash** can be thought of as a digital fingerprint for a file.

Hashes are used to verify the integrity of evidence.

If the hash of the original evidence matches the hash of the forensic copy, it provides evidence that the copy is identical to the original.

Hashes can also be checked later to determine whether evidence has changed.

### Key Principle:

> **Matching hashes help verify that evidence has not been altered.**

---

# 8. Chain of Custody

The **chain of custody** is a documented record showing how evidence has been handled.

It records information such as:

- Who collected the evidence
- When it was collected
- Who handled it
- When it was transferred
- Where it was stored
- What actions were performed

An unbroken chain of custody helps demonstrate that the evidence was properly handled and protected from unauthorised modification.

---

# 9. Investigation vs Digital Forensics

A normal cybersecurity investigation focuses on understanding suspicious activity.

Digital forensics adds additional discipline.

| Investigation | Digital Forensics |
|---|---|
| Focuses on understanding events | Focuses on understanding events |
| Analyses available evidence | Analyses available evidence |
| May have less formal evidence handling | Requires rigorous evidence handling |
| Used to investigate suspicious activity | Findings should be reliable and defensible |

### Simple Difference:

> **Digital Forensics = Investigation + Evidence Handling + Rigour**

---

# 10. DFIR as a Cybersecurity Career

**DFIR** stands for:

> **Digital Forensics and Incident Response**

It combines two areas of cybersecurity.

### Incident Response

Incident Response focuses on:

- Detecting an incident
- Containing the threat
- Removing the attacker
- Recovering affected systems

### Digital Forensics

Digital Forensics focuses on:

- Collecting evidence
- Preserving evidence
- Investigating the incident
- Building timelines
- Determining the impact
- Documenting findings

DFIR professionals may investigate major cyber incidents and communicate their findings to technical teams, management, legal professionals, and other stakeholders.

---

# 11. Tools Used in Network Forensics

## Wireshark

Wireshark can be used to analyse:

- Packets
- Network conversations
- IP addresses
- Protocols
- Suspicious traffic

The packet analysis skills I learned earlier in the Networks track provide a foundation for network forensic investigations.

---

## SIEM

A SIEM can help investigators:

- Search logs
- Find related security events
- Correlate activity
- Identify suspicious behaviour
- Build an incident timeline

A SIEM's searchable collection of security events can often provide an important starting point for an investigation.

---

# 12. Practical Exercise — Reconstructing an Incident

Today's practical exercise involved reconstructing an attack timeline using evidence collected from five different sources.

The events were initially presented out of chronological order.

After analysing the timestamps, the correct timeline was:

| Time | Event |
|---|---|
| **13:58** | A suspicious email attachment was opened |
| **14:05** | Successful login from a previously unknown device |
| **14:18** | Internal port scanning detected |
| **14:32** | Full customer database table exported |
| **14:40** | 240 MB transferred to an unexpected external IP |

---

# 13. Reconstructed Incident Story

The evidence suggested the following sequence of events:

1. A suspicious email attachment was opened.
2. The account was accessed from an unknown device.
3. Internal network scanning was detected from the user's workstation.
4. The full customer database table was exported.
5. A large amount of data was transferred to an external IP address.

The reconstructed attack flow was:

> **Suspicious Activity → Unauthorised Access → Internal Reconnaissance → Data Access → Possible Data Exfiltration**

However, an important forensic lesson is to avoid making assumptions beyond the available evidence.

For example, although the suspicious attachment appeared before the other events, the available evidence did not prove that it was the actual cause of the compromise.

Additional evidence would be required to confirm the initial access method.

---

# 14. Evidence Gaps Identified

One important source of evidence I would want is **endpoint or system logs from the affected workstation**.

These logs could help answer:

- Did the suspicious attachment execute?
- Was malware installed?
- What processes were running?
- Was the workstation compromised?
- Did the attacker establish persistence?

Other unanswered questions include:

- How were the credentials obtained?
- Was the suspicious attachment actually the initial access method?
- What exactly was included in the outbound data transfer?
- Did the attacker access other systems?
- Is the attacker still present in the network?
- Did the attacker create a backdoor or persistence mechanism?

This demonstrated an important principle of forensic investigation:

> **Evidence may strongly suggest something, but investigators should not treat assumptions as facts.**

---

# 15. Key Takeaways

- Network forensics reconstructs cyber incidents using logs, packet captures, and security alerts.
- The main output of a forensic investigation is an accurate timeline.
- Investigators need to determine how the attacker entered, what they did, what they accessed, whether they remain in the environment, and when events occurred.
- Synchronised clocks are essential for placing events in the correct order.
- Original evidence should be preserved, while analysis should be performed on verified copies.
- Cryptographic hashes help verify evidence integrity.
- Chain of custody documents who handled evidence and when.
- DFIR combines Digital Forensics and Incident Response.
- Good logging before an incident is essential for understanding what happened afterward.
- Investigators should follow the evidence and avoid making assumptions that cannot be supported.

---

# Conclusion

Today I learned that **Network Forensics is the process of turning separate pieces of digital evidence into a reliable story of a cyber incident**.

Logs, packet captures, and security alerts may individually show only small parts of an attack. When they are combined into an accurate timeline, they can reveal how an attacker entered, what actions they performed, what data was accessed, and what happened next.

I also learned that forensic investigation requires discipline beyond normal investigation. Evidence must be preserved, verified, and properly documented so that the findings remain trustworthy and defensible.

### Final Takeaway:

> **You can only reconstruct what the evidence recorded.**

This makes good logging, accurate timestamps, synchronised clocks, and proper evidence handling essential parts of cybersecurity preparation.