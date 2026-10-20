# Day 72 — MITRE ATT&CK

**MyFirstHack 90-Day Journey**

---

## Topic

**MITRE ATT&CK — Mapping Real Attacker Techniques**

Day 72 focused on MITRE ATT&CK and how it provides a more detailed view of attacker behaviour than a high-level framework such as the Cyber Kill Chain.

---

# 1. What Is MITRE ATT&CK?

**MITRE ATT&CK** is a publicly available knowledge base that documents real-world adversary tactics and techniques.

It helps defenders understand:

- What attackers are trying to achieve
- How attackers accomplish those goals
- Which techniques may appear during an attack
- Where defensive monitoring and detection may have gaps

While the Cyber Kill Chain provides a high-level view of an attack, ATT&CK provides much more detail about the specific behaviours used by attackers.

---

# 2. Cyber Kill Chain vs MITRE ATT&CK

The two frameworks are useful for different levels of analysis.

### Cyber Kill Chain

The Kill Chain describes an attack as a sequence of broad stages.

It answers:

> **“Where is the attacker in the attack?”**

For example:

- Reconnaissance
- Weaponization
- Delivery
- Exploitation
- Installation
- Command and Control
- Actions on Objectives

It gives a **high-level view** of how an attack progresses.

### MITRE ATT&CK

ATT&CK provides a detailed map of attacker behaviour.

It answers:

> **“What specific technique is the attacker using?”**

For example, an attacker may establish persistence using a scheduled task or create a malicious account.

### Simple comparison

**Kill Chain = high-level attack sequence**

**ATT&CK = detailed attacker techniques and behaviours**

The Kill Chain can show the overall story, while ATT&CK can help explain the specific methods used within that story.

---

# 3. Tactics

A **tactic** represents the attacker's goal or objective.

It answers:

> **“Why is the attacker doing this?”**

Examples of ATT&CK tactics include:

- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Collection
- Command and Control
- Exfiltration
- Impact

A tactic describes the attacker's **purpose**, rather than the exact method.

---

# 4. Techniques

A **technique** describes the specific method an attacker uses to achieve a goal.

It answers:

> **“How is the attacker doing this?”**

For example:

### Tactic: Persistence

An attacker wants to maintain access to a system.

Possible techniques include:

- Creating a malicious account
- Using a scheduled task
- Establishing another persistence mechanism

The tactic describes the **goal**.

The technique describes the **method**.

---

# 5. Tactic vs Technique

A useful way to remember the difference is:

**Tactic = WHY**

**Technique = HOW**

### Example

An attacker wants to maintain access to a compromised system.

**Tactic:** Persistence

**Technique:** Create a scheduled task to execute malicious code automatically.

Another example:

**Tactic:** Command and Control

**Technique:** Establish communication between a compromised system and an attacker-controlled server.

---

# 6. Sub-Techniques

Some ATT&CK techniques are divided into **sub-techniques**.

Sub-techniques provide additional detail about exactly how a technique is performed.

This allows ATT&CK to represent attacker behaviour at a more specific level rather than grouping many different behaviours into one broad category.

---

# 7. The ATT&CK Matrix

The MITRE ATT&CK matrix organises attacker behaviour according to tactics.

It allows defenders to view attacker objectives alongside the techniques that may be used to achieve them.

A simplified way to understand the structure is:

**Tactic → Technique → Specific attacker behaviour**

For example:

**Persistence → Scheduled Task/Job → Attacker uses a scheduled task to maintain execution**

The matrix can be used as a reference when analysing incidents, developing detections, or reviewing defensive coverage.

---

# 8. Why ATT&CK Is Useful

## Detection Coverage

Security teams can compare their existing detections against known attacker techniques.

This helps identify:

- Techniques that are already monitored
- Techniques with weak detection
- Techniques with no detection
- Blind spots in security monitoring

## Common Language

ATT&CK provides a common vocabulary for describing attacker behaviour.

Instead of different teams describing the same activity in different ways, analysts can refer to recognised tactics and techniques.

This can improve communication between:

- SOC analysts
- Incident responders
- Threat intelligence teams
- Security engineers
- Red teams
- Blue teams

## Threat Intelligence

ATT&CK can help analysts understand how known adversaries operate and which techniques they commonly use.

This provides useful context when investigating suspicious activity.

## Red and Blue Team Exercises

### Red teams

Can use ATT&CK techniques to simulate realistic attacker behaviour.

### Blue teams

Can use those techniques to test:

- Detection
- Monitoring
- Logging
- Response capabilities

## SOC Analyst Work

SOC analysts can use ATT&CK concepts when:

- Investigating alerts
- Analysing suspicious activity
- Classifying attacker behaviour
- Writing incident reports
- Identifying detection gaps

---

# 9. Examples of Mapping Attacker Behaviour to ATT&CK

### Hidden Scheduled Task

An attacker creates a hidden scheduled task to maintain access or execute malicious activity.

**Tactic:** Persistence

**Technique:** Scheduled Task/Job

### New Attacker-Controlled Account

An attacker creates or abuses an account to maintain access.

**Tactic:** Persistence

**Technique:** Account-related persistence technique

### Malware Communicating With an Attacker Server

A compromised machine connects to an attacker-controlled server to receive commands.

**Tactic:** Command and Control

**Technique:** A technique describing the communication method used by the malware.

### Covering Tracks

An attacker attempts to remove or hide evidence of their activity.

**Tactic:** Defense Evasion

**Technique:** A technique for removing or modifying evidence.

---

# 10. ATT&CK in Security Analysis

ATT&CK becomes especially useful when an analyst moves beyond simply saying:

> “An attacker compromised the system.”

Instead, the analyst can ask:

- What was the attacker trying to achieve?
- Which tactic does this behaviour represent?
- What technique did the attacker use?
- Is there a more specific sub-technique?
- Would our security controls detect this behaviour?
- Where are our monitoring gaps?

This turns an incident description into a more structured technical analysis.

---

# 11. Connecting ATT&CK With Previous Learning

MITRE ATT&CK builds on earlier concepts in the MyFirstHack journey.

### Cyber Kill Chain

Helps understand the **overall attack sequence**.

### MITRE ATT&CK

Helps identify the **specific techniques and behaviours** used within that sequence.

### Threat Modeling

Helps consider **who might attack and why**.

Together, these concepts provide different perspectives on the same attack.

---

# 12. Day 72 Tasks

## Task 1 — Define ATT&CK

Write a **one-sentence definition of MITRE ATT&CK**.

A strong definition should explain that ATT&CK is a knowledge base of real-world adversary tactics and techniques used to understand and defend against attacker behaviour.

## Task 2 — Tactic vs Technique

Give an example that clearly demonstrates the difference between a tactic and a technique.

For example:

**Tactic:** Persistence

**Technique:** Using a scheduled task to maintain execution or access.

The goal is to demonstrate:

**Tactic = WHY**

**Technique = HOW**

## Task 3 — Explore the ATT&CK Matrix

Optionally browse the MITRE ATT&CK matrix and become familiar with how tactics and techniques are organised.

Focus on understanding the structure rather than trying to memorise every technique.

## Task 4 — Map Previous Knowledge to ATT&CK

Take examples from previous cybersecurity learning and identify the ATT&CK tactic they could relate to.

Examples:

- Hidden scheduled task → **Persistence**
- New attacker-controlled account → **Persistence**
- Malware connecting to an attacker server → **Command and Control**
- Covering tracks → **Defense Evasion**

The purpose is to practise recognising attacker behaviour through an ATT&CK perspective.

---

# 13. Key Takeaways

- **MITRE ATT&CK is a public knowledge base of real-world adversary tactics and techniques.**
- The **Cyber Kill Chain provides a high-level view** of an attack sequence.
- **ATT&CK provides more detailed information** about specific attacker behaviours.
- A **tactic describes the attacker's goal or WHY**.
- A **technique describes the method or HOW**.
- **Sub-techniques** provide additional detail about specific techniques.
- ATT&CK can help security teams identify **detection gaps and blind spots**.
- ATT&CK provides a **common language** for SOC analysts, incident responders, threat intelligence teams, and security testers.
- Analysts can use ATT&CK to connect observed behaviour to known attacker techniques.
- Understanding ATT&CK is useful for **detection, threat intelligence, incident response, red/blue team exercises, and SOC analysis**.
- The combination of **Kill Chain + ATT&CK** provides a stronger understanding of both the overall attack sequence and the specific techniques used within it.

---

# Day 72 Summary

The key shift from the Cyber Kill Chain to MITRE ATT&CK is moving from a **high-level view of where an attack is in its lifecycle** to a **detailed view of how an attacker actually behaves**.

**Kill Chain → What stage is the attack in?**

**ATT&CK → What specific technique is the attacker using?**

Understanding both makes it easier to analyse attacks, communicate attacker behaviour, and identify where defensive coverage can be improved.

---

**MyFirstHack 90-Day Journey — Day 72/90**
