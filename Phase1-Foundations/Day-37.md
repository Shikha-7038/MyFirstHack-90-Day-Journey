# Day 37 — SIEM, Correlation & SOAR

**Challenge:** 90 Days of Cybersecurity with MyFirstHack  
**Day:** 37  
**Topic:** Security Information and Event Management (SIEM), Correlation Logic, and SOAR

---

## Overview

Today's learning focused on **SIEM (Security Information and Event Management)** and its role in a **Security Operations Centre (SOC)**.

Security systems across an organisation generate huge amounts of logs and alerts every day. These can come from firewalls, IDS/IPS, servers, employee devices, cloud services, applications, and authentication systems.

The challenge is that a real attack can be hidden among thousands of normal or low-priority events.

A SIEM helps solve this problem by collecting security data into one place, normalising different log formats, correlating related events, generating alerts, and supporting investigations.

The most important concept I learned today was **correlation**: connecting multiple events to identify patterns that a single event cannot reveal.

---

# What is a SIEM?

**SIEM** stands for:

> **Security Information and Event Management**

A SIEM is a central platform that collects and analyzes security-related logs and events from across an organisation.

It can be thought of as the **central nervous system of a SOC**.

Instead of analysts manually checking many different systems, a SIEM brings relevant security information together.

### Common data sources include:

- Firewalls
- IDS/IPS
- Servers
- Employee endpoints
- Authentication systems
- Cloud services
- Applications
- Email security systems
- Network devices

---

# Why is a SIEM Needed?

Without a SIEM, security information may be scattered across many systems.

An analyst might need to investigate:

```text
Firewall Logs
      +
Server Logs
      +
Endpoint Logs
      +
Authentication Logs
      +
Cloud Logs
      =
Difficult Investigation
```

A SIEM centralizes this information:

```text
Firewall ───────┐
IDS/IPS ────────┤
Servers ────────┤
Endpoints ──────┼──> SIEM ───> SOC Analyst
Cloud Services ─┤
Applications ───┘
```

This makes security data easier to search, investigate, and correlate.

---

# Core Functions of a SIEM

## 1. Collection

The SIEM collects logs and security events from different systems.

Examples include:

- Failed login attempts
- Successful logins
- Firewall activity
- Malware detections
- Network connections
- Cloud activity
- Application events

### Important principle:

> **No logs = No visibility.**

If a system is not sending logs to the SIEM, the SIEM cannot monitor activity happening on that system.

---

## 2. Normalisation

Different systems produce logs in different formats.

For example, Windows, Linux, firewalls, and cloud services may all record login events differently.

**Normalisation** converts different log formats into a common structure.

This allows analysts and the SIEM to:

- Search across different systems
- Compare events
- Identify related activity
- Perform correlation

### Simple explanation:

> **Normalisation makes different systems speak the same language.**

---

## 3. Correlation

Correlation is one of the most valuable functions of a SIEM.

It connects multiple events and looks for suspicious patterns.

A single event may not be important, but several related events can indicate an attack.

### Example:

```text
One Failed Login
        ↓
Usually Normal

Many Failed Logins
        +
Successful Login
        ↓
Possible Brute-Force Attack
```

### Simple definition:

> **Correlation means connecting related events to identify patterns that may indicate a security incident.**

---

# Correlation Logic Lab

Today's lab involved thinking like a SIEM and manually designing correlation logic.

The goal was to understand how raw events can be turned into meaningful alerts.

---

## Step 1 — Separating Noise from Signal

The following events were evaluated individually.

| Event | Alert-Worthy Alone? | Reason |
|---|---|---|
| Single failed login | No | A user may have entered the wrong password. |
| Successful login from a normal location during work hours | No | Normal expected activity. |
| Connection to a known malicious IP | Yes | May indicate communication with malicious infrastructure and should be investigated. |
| Antivirus detection automatically quarantined | Usually No | The threat was automatically contained, though the event should still be logged. |
| Firewall blocks one inbound connection attempt | No | One blocked connection is common and does not necessarily indicate an active attack. |

### Key lesson:

> **A single event is often noise. Multiple connected events can become a meaningful signal.**

---

# Step 2 — Correlation Rules

## Brute-Force Detection

**IF** the same account experiences many failed login attempts followed by a successful login **WITHIN** a short period of time **THEN** generate a high-priority alert for a possible brute-force attack or account compromise.

---

## Credential Stuffing Detection

**IF** the same source IP attempts to log into many different accounts, with multiple failed attempts and some successful logins, **WITHIN** a short period of time **THEN** generate an alert for possible credential stuffing.

---

## Impossible Travel Detection

**IF** the same account successfully logs in from two geographically distant locations within a time period that makes physical travel impossible **THEN** generate an alert for possible account compromise.

### Example:

```text
London Login
       ↓
10 Minutes Later
       ↓
Singapore Login
       ↓
Possible Impossible Travel Alert
```

---

# Step 3 — Correlating a Full Attack Chain

The following events were received from five different systems.

### Event 1 — Email Security

A user received and opened an email with a flagged attachment.

### Event 2 — Authentication

The user's account logged in from a device that had never been seen before.

### Event 3 — IDS

Internal network scanning was detected from the user's workstation.

### Event 4 — Database

The user's account accessed a customer records database it had never accessed before.

### Event 5 — Firewall

A large outbound data transfer occurred from the workstation to an external IP address.

---

## The Correlated Attack Story

When viewed individually, these events may not always appear to be a confirmed attack.

However, when correlated, they tell a possible attack story:

```text
Suspicious Email
        ↓
Possible Device or Account Compromise
        ↓
Login From New Device
        ↓
Internal Network Scanning
        ↓
Unusual Database Access
        ↓
Large Outbound Data Transfer
        ↓
Possible Data Exfiltration
        ↓
Possible Security Breach
```

The possible sequence is:

1. The user opens a suspicious attachment.
2. The user's device or account may become compromised.
3. The attacker performs internal reconnaissance.
4. Sensitive customer data is accessed.
5. Data may be transferred outside the organisation.

This should be treated as a serious security incident requiring investigation.

---

# Why Individual Events Could Be Missed

Each event alone could have a legitimate explanation.

### Suspicious Email

The email may have been flagged but not necessarily resulted in a successful compromise.

### Login From a New Device

The user may simply be using a new computer.

### Internal Network Scanning

The activity could potentially be caused by an administrator or authorized security tool.

### Unusual Database Access

The user may have been given new access for legitimate work.

### Large Data Transfer

The transfer could be related to backups or other business activity.

---

## Why Correlation Changes Everything

When these events occur in sequence and involve the same user or workstation, the overall context changes.

```text
Suspicious Email
        +
New Device Login
        +
Network Scanning
        +
Unusual Database Access
        +
Large Data Transfer
        =
Possible Data Breach
```

### Key lesson:

> **One event is a clue. Multiple connected events tell an attack story.**

This demonstrates the real power of SIEM correlation.

---

# Step 4 — Finding Logging Gaps

A SIEM is blind to systems that are not sending it logs.

For a small business, important log sources include:

## 1. Authentication and Email Systems

These logs can help identify:

- Failed login attempts
- Suspicious logins
- Account compromise
- Password changes
- Email-based threats

---

## 2. Endpoints and Employee Devices

Endpoint logs can help identify:

- Malware
- Suspicious processes
- Device compromise
- Unusual activity

---

## 3. Firewall and Network Devices

These logs can help identify:

- Suspicious inbound connections
- Malicious IP communication
- Blocked traffic
- Large outbound transfers
- Possible data exfiltration

---

## Consequence of a Logging Gap

If a critical system silently stops sending logs, the SIEM loses visibility into that system.

For example:

```text
Critical System Activity
        ↓
Logs Stop Being Sent
        ↓
SIEM Has No Visibility
        ↓
Suspicious Activity May Go Undetected
```

### Important principle:

> **If the SIEM does not receive the logs, it cannot detect activity from those logs.**

---

# Alerting and Investigation

After detecting suspicious patterns, the SIEM can generate alerts.

Alerts may be prioritised by severity:

- Critical
- High
- Medium
- Low

SOC analysts can then investigate the alert by searching and reviewing events across multiple systems.

For example:

> What did this user do during the last 24 hours?

The SIEM can help collect information from authentication systems, endpoints, servers, firewalls, and cloud platforms.

---

# Limitations of SIEM

A SIEM is powerful, but it is not magic.

Its effectiveness depends on:

## Log Coverage

Missing logs create blind spots.

## Detection Rules

Poor correlation rules can result in missed attacks.

## Continuous Tuning

False positives can create alert fatigue.

## Skilled Analysts

SIEM tools help analysts work more effectively but do not replace human judgement.

### Simple summary:

> **A SIEM is only as good as the data it receives, the rules it uses, and the people operating it.**

---

# SIEM and SOAR

Today I also learned about **SOAR**.

**SOAR** stands for:

> **Security Orchestration, Automation, and Response**

A simple comparison:

| SIEM | SOAR |
|---|---|
| Collects security data | Automates workflows |
| Normalizes logs | Connects security tools |
| Correlates events | Runs response playbooks |
| Generates alerts | Automates response actions |
| Supports investigation | Helps respond faster |

---

## Example SOAR Workflow

```text
SIEM Detects Suspicious Activity
        ↓
SOAR Playbook Starts
        ↓
Block Malicious IP
        ↓
Disable Compromised Account
        ↓
Isolate Affected Device
        ↓
Create Incident Ticket
        ↓
Notify Security Team
```

Not every response should be automated, but routine and well-defined actions can often be handled through playbooks.

---

# Major SIEM Platforms

Some major SIEM platforms include:

- Splunk
- Microsoft Sentinel
- Elastic Security
- IBM QRadar
- Google Security Operations

Although platforms differ, the main concepts remain similar.

---

# Complete Security Operations Workflow

```text
Security Systems
        ↓
Collect Logs
        ↓
Normalize Data
        ↓
Correlate Events
        ↓
Generate Alerts
        ↓
SOC Investigation
        ↓
Response / SOAR Automation
        ↓
Contain the Threat
```

---

# Key Takeaways

- A **SIEM** centralizes security logs and alerts.
- **Collection** gathers information from different systems.
- **Normalisation** converts different log formats into a common structure.
- **Correlation** connects events and identifies suspicious patterns.
- A single event may be noise, while multiple related events may reveal an attack.
- Missing logs create dangerous **blind spots**.
- SIEM rules require continuous tuning to reduce **false positives**.
- **SIEM helps detect and investigate threats**.
- **SOAR helps automate parts of the response**.
- A SIEM is a **force multiplier for skilled security analysts**, not a replacement for them.

---

# My Biggest Learning

> **The real power of a SIEM is not simply collecting thousands of logs. Its real value comes from connecting events that may look harmless individually and revealing the bigger attack story.**

### Easy Way to Remember

```text
Collect
   ↓
Normalize
   ↓
Correlate
   ↓
Alert
   ↓
Investigate
   ↓
Respond
```

---

**Day 37 Complete. ✅**