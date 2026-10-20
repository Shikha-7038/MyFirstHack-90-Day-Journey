# 🛡️ Day 18 — How Attacks Actually Work

**Day:** 18 of 90  
**Date:** 10 August 2026  
**Journey:** MyFirstHack 90-Day Cybersecurity Journey  
**Main Topic:** Cyber Kill Chain, MITRE ATT&CK & Attack Analysis

---

## 🎯 Today's Objective

Today I moved from looking at cybersecurity mainly from the **defender's perspective** to understanding how an attacker approaches a target.

The main goals for today were:

- Understand how real cyber attacks are structured.
- Learn the **Cyber Kill Chain**.
- Understand how defenders can interrupt an attack.
- Map a real-world breach to the Kill Chain.
- Learn the basics of **MITRE ATT&CK**.
- Identify specific MITRE ATT&CK techniques used in a real incident.
- Apply the Kill Chain to my own primary email account.

---

## 🧠 1. Understanding the Attacker's Perspective

Before today, I mostly looked at cybersecurity from the question:

> **"How can I protect this system?"**

Today I started asking another question:

> **"If I were an attacker, what would I do next?"**

This change in perspective is important because an attacker usually doesn't start by immediately stealing data.

There can be several steps before the actual damage happens:

**Information gathering → gaining access → establishing control → moving toward the target → stealing or damaging something**

### My Understanding

An attack is not necessarily one single action.

It is better to think of it as a **chain of activities**, where breaking one important link can prevent the attacker from reaching their final objective.

---

# ⛓️ 2. Cyber Kill Chain

The Cyber Kill Chain is a framework used to describe the stages of a targeted cyber attack.

The seven stages are:

1. **Reconnaissance**
2. **Weaponisation**
3. **Delivery**
4. **Exploitation**
5. **Installation**
6. **Command & Control**
7. **Actions on Objectives**

I learned that these stages are useful because they give defenders different opportunities to detect or stop an attacker.

---

## 🔎 Stage 1 — Reconnaissance

This is where the attacker gathers information about the target.

Information might include:

- Names
- Email addresses
- Technologies being used
- Employees
- Publicly available documents
- Social media information
- Exposed services

### What I Understood

The attacker may be learning about the target **before the target even knows an attack is happening**.

This made me realise that publicly available information can become part of someone's attack surface.

---

## 🛠️ Stage 2 — Weaponisation

The attacker prepares something that can be used against the target.

Examples include:

- Phishing content
- Malicious documents
- Exploits
- Fake login pages
- Malware

### What I Understood

The attack is prepared based on information gathered during reconnaissance.

The weapon does not always have to be sophisticated malware. Sometimes a carefully crafted request or fake login page can be enough.

---

## 📤 Stage 3 — Delivery

The attacker sends or delivers the attack to the target.

Possible delivery methods include:

- Email
- SMS
- Malicious websites
- Social media messages
- USB devices
- Exploited public-facing services

### What I Understood

Delivery is the point where the attack reaches the target environment.

---

## 💥 Stage 4 — Exploitation

This is when the attacker takes advantage of something to gain access.

It could involve:

- A software vulnerability
- A stolen credential
- A malicious link
- A malicious attachment
- A misconfiguration
- A vulnerable public-facing application

### What I Understood

This is an important stage because it can be the point where an attacker changes from **trying to get in** to actually having access.

---

## 📥 Stage 5 — Installation

The attacker tries to establish persistence or maintain access.

This could involve:

- Malware
- Backdoors
- Scheduled tasks
- Modified authentication settings
- Other persistence mechanisms

### What I Understood

Persistence is important because an attacker may want to remain inside even after a restart or other temporary change.

However, I also learned that **not every attack requires traditional installation or persistence**.

---

## 📡 Stage 6 — Command & Control

After gaining access, an attacker may need a way to communicate with compromised systems.

This can allow them to:

- Send commands
- Receive information
- Control compromised systems
- Maintain communication with their infrastructure

### What I Understood

This stage is particularly important for SOC analysts because unusual communication can provide evidence that a system has already been compromised.

---

## 🎯 Stage 7 — Actions on Objectives

This is when the attacker finally performs what they originally wanted to accomplish.

Examples include:

- Stealing data
- Encrypting files
- Destroying information
- Moving to other systems
- Financial theft
- Data exfiltration

### My Understanding

The visible damage usually happens here, but the attacker may have been working through the earlier stages for much longer.

---

# 🛡️ 3. The Main Defender Lesson — Break the Chain

One of the most important things I learned today was:

> **A defender does not have to wait until the final stage to stop an attack.**

If an attack is detected during:

- Reconnaissance
- Delivery
- Exploitation
- Persistence
- Command & Control

then the attacker may never reach the final objective.

This is why security controls are placed at different layers.

For example:

**Phishing detection → Endpoint security → Authentication controls → Network monitoring → Data protection**

No single security control is perfect, so multiple layers provide multiple opportunities to stop an attacker.

---

# 🔬 4. Practical Task — Mapping a Real Breach

For today's practical exercise, I selected the **PowerSchool breach** and used the information from the investigation to understand how the incident could be viewed through the Cyber Kill Chain.

Initially, I found the investigation report overwhelming because it contained a lot of information.

Instead of trying to understand every detail, I focused on the information needed for the seven Kill Chain stages.

This was an important learning experience because it taught me that when reading a large incident report, I don't necessarily need to understand **everything**.

I need to first identify:

> **What happened, how access was obtained, what the attacker did, and what information was affected?**

---

# 🧩 5. PowerSchool Breach — Kill Chain Analysis

## Stage 1 — Reconnaissance 🔎

**Finding:** Not clearly established in the investigation information I reviewed.

I could not find enough reliable information to say exactly what reconnaissance the attacker performed before the compromise.

### My Approach

Instead of assuming what the attacker must have done, I recorded this as **unknown/not established**.

---

## Stage 2 — Weaponisation 🛠️

**Finding:** No specific weaponisation method was clearly established.

The available investigation information did not provide enough evidence for me to identify a particular malware, exploit, or weapon that was prepared before the attack.

### What I Learned

A Kill Chain analysis does not mean every stage must have a clear answer.

Some stages can remain unknown.

---

## Stage 3 — Delivery 📤

**Finding:** The attacker used compromised legitimate credentials.

However, the information I reviewed did not clearly establish **how those credentials were originally obtained**.

Therefore, I did not assume a phishing attack or another delivery method without evidence.

### Important Lesson

This was one of the places where I learned to separate:

**What the report proves**

from

**What I think might have happened.**

---

## Stage 4 — Exploitation / Initial Access 💥

This was one of the most important stages in my analysis.

The attacker used compromised support credentials to access the PowerSource portal and then use the available Maintenance Access functionality.

This provided a path into the PowerSchool environment.

### What I Understood

The initial compromise did not necessarily have to involve malware.

**Valid credentials themselves can become the entry point.**

---

## Stage 5 — Installation 📥

**Finding:** No traditional malware installation or persistence mechanism was identified from the information I reviewed.

The attacker did not necessarily need to install malware to accomplish the objective.

### What I Learned

This helped me understand that:

> **No malware does not automatically mean no attack.**

An attacker using legitimate credentials can sometimes operate through existing systems and legitimate functionality.

---

## Stage 6 — Command & Control 📡

**Finding:** I did not identify a traditional malware-based C2 channel from the investigation information.

The activity involved the attacker using legitimate web-based functionality rather than the classic pattern of malware communicating with an attacker's command server.

### What I Learned

The traditional Kill Chain model does not always fit perfectly into modern attacks.

Attackers can abuse legitimate accounts and legitimate services instead of creating an obvious C2 channel.

---

## Stage 7 — Actions on Objectives 🎯

The final objective involved accessing and extracting sensitive information from customer student information systems.

The affected information included student and teacher-related data.

### What I Understood

This was the stage where the attacker's objective became visible through the access and extraction of data.

---

# 🧠 6. Important Lesson From the PowerSchool Analysis

One of my biggest lessons from this practical task was:

> **Do not fill gaps in an investigation with assumptions.**

At first, I felt that every Kill Chain stage should have a clear answer.

But after working through the PowerSchool investigation, I understood that a professional analysis can contain:

- **Confirmed**
- **Unknown**
- **Not established**
- **Not applicable**

That is much better than creating an answer that the evidence doesn't support.

---

# 🗺️ 7. MITRE ATT&CK

After understanding the Kill Chain, I learned about **MITRE ATT&CK**.

The biggest difference I understood is:

### Cyber Kill Chain

Focuses on the **overall stages of an attack**.

### MITRE ATT&CK

Provides a much more detailed description of **attacker behaviour and techniques**.

MITRE ATT&CK uses:

- **Tactics** → What the attacker is trying to achieve.
- **Techniques** → How the attacker achieves it.

Techniques have specific IDs, which makes it easier for security professionals to communicate about attacker behaviour consistently.

---

# 🔍 8. MITRE ATT&CK Techniques I Identified

During my PowerSchool analysis, I identified techniques relevant to the incident.

## T1078 — Valid Accounts

The attacker used legitimate credentials that had been compromised.

The important idea here is that the attacker did not necessarily need to exploit a software vulnerability if they already had valid credentials.

### My Understanding

A legitimate username and password can still be dangerous when they are being used by the wrong person.

---

## T1213 — Data from Information Repositories

This technique relates to obtaining information from repositories where useful data is stored.

In this case, the attacker accessed information stored within the affected PowerSchool customer environments.

### My Understanding

This helped me connect the final objective of the breach with a specific MITRE ATT&CK technique rather than describing the activity only in general terms.

---

# 🧪 9. Personal Exercise — Running the Kill Chain Against Myself

After analysing the PowerSchool incident, I applied the same thinking to my own digital life.

I selected my:

> **Primary email account**

I selected this account because email can be extremely important for account recovery and can be connected to many other online services.

---

# 🔎 10. My Personal Kill Chain

## Stage 1 — Reconnaissance

I considered what a stranger could learn about me through public sources such as:

- Search engines
- LinkedIn
- Instagram
- Public professional information
- Public cybersecurity learning activity

### Possible Attack Scenario

An attacker could collect information about my interests, education, cybersecurity learning, and other publicly available details.

### Defence

Reduce unnecessary personal information exposed publicly.

---

## Stage 2 — Weaponisation

Based on the information collected, an attacker could prepare a believable social-engineering message.

For example, they could make a message related to:

- Internship opportunities
- Courses
- Certificates
- Account verification

### Defence

Verify unexpected requests independently rather than trusting the identity shown in the message.

---

## Stage 3 — Delivery

The attack could be delivered through:

- Email
- LinkedIn
- SMS
- Social media

For me, email or a professional platform could be a realistic channel.

### Defence

Be careful with unexpected links and attachments.

---

## Stage 4 — Exploitation

The attacker could try to convince me to click a realistic-looking login or verification link.

### Defence

Instead of using a login link from an unexpected message, open the official website or application separately.

---

## Stage 5 — Installation / Persistence

If an attacker gained access to my email, they could potentially try to maintain access through:

- Recovery settings
- Authentication methods
- Connected applications
- Active sessions

### Defence

Regularly review account recovery settings, connected apps, authentication methods, and logged-in devices.

---

## Stage 6 — Command & Control 📡

This became my **weakest stage**.

I realised that even if I could identify a suspicious login, I might not immediately notice hidden changes such as:

- Email forwarding rules
- Filters
- Other account changes
- Unauthorized connected applications

An attacker could potentially use these mechanisms to monitor or hide activity.

### Defence

Regularly review:

- Email forwarding
- Filters
- Connected applications
- Active sessions
- Account activity

---

## Stage 7 — Actions on Objectives

If an attacker gained control of my primary email, they could potentially try to:

- Reset other accounts
- Access information
- Impersonate me
- Target other services connected to the email

### Defence

Use strong, unique passwords and MFA on important accounts, especially the primary email.

---

# ⚠️ 11. My Weakest Area

## Stage 6 — Command & Control

This was the stage I identified as my personal weak point.

The reason is that I may be more focused on preventing an attacker from getting into my account than checking whether someone has **already gained access and quietly changed something**.

My main concern is not just:

> "Can someone log in?"

but also:

> **"Would I notice if someone was already inside?"**

This changed the way I think about account security.

---

# 🛡️ 12. Defence I Plan to Use

One practical defence I identified is to regularly review my primary email account for unexpected changes.

I can check:

- Active sessions
- Recent login activity
- Forwarding addresses
- Email filters
- Connected applications
- Recovery options
- Authentication methods

This gives me a way to detect some forms of unauthorized access that might otherwise remain unnoticed.

---

# 📚 13. What I Learned Today

### 1. Attacks Follow Patterns

I learned that attacks are usually not one random action. They can involve several stages.

### 2. The Final Damage Is Not the Beginning

The visible damage may happen at the end, while reconnaissance and initial access happened much earlier.

### 3. The Kill Chain Is a Defender's Tool

It helps defenders identify where an attack can be interrupted.

### 4. Not Every Stage Will Always Be Visible

A real investigation can contain unknown or unconfirmed stages.

### 5. Evidence Is More Important Than Assumptions

If an investigation does not establish something, I should record it as unknown rather than inventing an explanation.

### 6. Legitimate Credentials Can Be Dangerous

An attacker does not always need malware or a sophisticated exploit. Compromised legitimate credentials can provide a powerful starting point.

### 7. MITRE ATT&CK Gives More Detail

The Kill Chain gives me the broader attack sequence, while MITRE ATT&CK helps describe specific attacker techniques.

### 8. I Need to Think Beyond Initial Access

My personal exercise showed me that protecting an account is not only about preventing login attempts. I also need to think about what happens **after an attacker gets access**.

---

# 💡 14. My Main Takeaway

The biggest change in my thinking today was:

> **Cybersecurity is not only about asking how to prevent an attacker from getting in. It is also about understanding what the attacker will do before, during, and after gaining access.**

The Cyber Kill Chain gave me a simple way to understand that process, while MITRE ATT&CK showed me how security professionals describe specific attacker behaviour.

Most importantly, I was able to take these frameworks beyond theory by applying them to a **real breach and my own primary email account**.

---

# 📝 Day 18 Summary

| Area | What I Completed |
|---|---|
| Cyber Kill Chain | Learned all 7 stages |
| Real-world analysis | Mapped the PowerSchool breach |
| MITRE ATT&CK | Identified T1078 and T1213 |
| Personal threat modelling | Applied the Kill Chain to my primary email |
| Weakest stage | Stage 6 — Command & Control |
| Defence identified | Review forwarding, filters, apps, sessions and account activity |
| Main lesson | Break the attack chain as early as possible |

---

## 🎯 Final Reflection

Today was different from simply learning a cybersecurity concept because I had to **use the framework to analyse something real**.

The PowerSchool investigation also taught me that security analysis can feel overwhelming when there is too much information. Instead of trying to understand every line, I learned to focus on the evidence relevant to the question I am trying to answer.

That is something I want to continue improving as I progress through my cybersecurity journey.