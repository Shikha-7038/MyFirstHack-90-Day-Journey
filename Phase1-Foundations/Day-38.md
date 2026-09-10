# Day 38 — Logs: The Foundation of Security Operations

**90-Day Cybersecurity Journey — MyFirstHack**

## Overview

Today I learned about **logs**, the foundation underneath security detection, SIEM correlation, and incident investigation.

A log is a record of an event that occurred on a system, application, or network. Examples include successful and failed logins, network connections, file access, service activity, configuration changes, and application errors.

The key idea from today's learning was:

> **You can't investigate what you didn't log.**

When a security incident occurs, logs are often the evidence investigators use to understand what happened. If an important event was never logged, the logs were deleted too early, or an attacker was able to erase them, reconstructing the incident becomes much more difficult.

---

# What I Learned

## 1. Logs Are the Raw Material of Security Operations

Everything in security operations begins with events being recorded.

The relationship between the technologies and processes I have been learning is:

**Event → Log → Detection → Alert → SIEM Correlation → Investigation**

- An event happens on a system or network.
- A log records that event.
- Detection systems identify suspicious activity.
- An alert is generated.
- A SIEM collects and correlates events from multiple sources.
- A security analyst investigates the evidence.

This helped me connect the previous topics I learned about IDS/IPS, SIEMs, and security investigations.

---

# 2. Types of Logs

Different log sources answer different investigation questions.

### Authentication Logs

Authentication logs record information about login activity, including:

- Account involved
- Time of the event
- Source information
- Successful or failed outcome

These logs are useful when investigating:

- Brute-force attacks
- Credential attacks
- Account compromise
- Suspicious login activity

---

### Network Logs

Network logs record communication between devices and systems.

They can include:

- Source and destination
- Ports
- Connection times
- Data transfer information

Examples include:

- Firewall logs
- NAT logs
- IDS/IPS logs
- Network flow logs

These logs help answer:

> **What communicated with what?**

---

### System and Event Logs

System logs record events occurring on a computer or server.

Examples include:

- Services starting or stopping
- Configuration changes
- Errors
- Crashes

On Windows, these are available through **Windows Event Viewer**.

These logs help answer:

> **What happened on this machine?**

---

### Application Logs

Application logs record activity inside specific software.

Examples include:

- Web server requests
- Database activity
- Email activity
- Application errors

These logs help answer questions about what happened inside a specific application.

---

### Audit Logs

Audit logs record important security-related or privileged actions.

Examples include:

- Accessing sensitive information
- Changing permissions
- Administrative actions

They are important for security investigations, insider threat monitoring, and compliance.

---

# 3. What Makes a Log Useful?

A useful log needs more than simply recording that an event occurred.

## Accurate and Synchronised Timestamps

Logs need accurate timestamps so events can be placed in the correct order.

Different systems also need synchronised clocks. Organisations commonly use **NTP (Network Time Protocol)** to keep system clocks aligned.

If systems disagree about the time, building an accurate timeline and correlating events across multiple systems becomes difficult.

---

## Enough Detail

A useful log should provide enough information to answer:

**Who → What → When → Where → Outcome**

However, logging should also be deliberate. Logging everything can create huge volumes of data, increase storage costs, and make it harder to find important events.

---

## Retention

Logs must be kept long enough for realistic investigations.

Security incidents may remain undetected for weeks or months. If logs are deleted before an incident is discovered, important evidence may no longer be available.

---

## Integrity

Logs should be protected from modification or deletion.

An attacker who compromises a machine may attempt to clear local logs to hide their activity.

This is one reason organisations use centralised logging.

---

# 4. Centralised Logging

Instead of keeping logs only on the device where they were created, organisations can send them to central storage or a SIEM.

**Device → Log Collection → Central Storage / SIEM**

Centralised logging provides several benefits:

- Collects logs from multiple systems
- Makes correlation easier
- Helps protect evidence
- Makes it harder for an attacker to erase all copies of the logs

If an attacker compromises a machine, they may be able to delete local logs. However, copies already sent to protected central storage are more difficult for the attacker to remove.

---

# 5. Reading Logs

Most logs can be understood as records of individual events.

A typical log entry can answer:

- Who was involved?
- When did it happen?
- What happened?
- Where did it come from?
- What was the outcome?

The important analytical skill is learning to identify patterns rather than treating every individual event as suspicious.

---

# 6. HTTP Status Codes in Log Analysis

I also learned that status codes can help analysts understand what a user or attacker may be doing.

### 404 — Not Found

A large number of 404 responses from the same source across many different paths could indicate reconnaissance or scanning for hidden resources.

### 401 — Unauthorized

Authentication is required.

### 403 — Forbidden

Access to a protected resource was denied.

Repeated 401 or 403 responses may indicate repeated attempts to access protected resources.

### 500 — Internal Server Error

The server or application experienced an error.

This could result from a normal application problem or potentially unexpected or malicious activity.

A single event does not necessarily prove an attack. Analysts look for patterns and context.

---

# 7. Log Investigation Process

The investigation process follows the same mindset I previously used when analysing network traffic.

### Orient

Understand the overall environment:

- What logs are available?
- What time period do they cover?
- What looks normal?

### Question

Identify something that appears unusual.

### Filter

Narrow the logs using information such as:

- User account
- IP address
- Event ID
- Event type
- Time period

### Read

Examine the relevant entries and understand the events.

### Conclude

Use the available evidence to determine what likely happened.

**Orient → Question → Filter → Read → Conclude**

---

# Hands-On Activity — Reading My Own Windows Logs

For today's practical exercise, I examined logs on my own Windows machine using **Windows Event Viewer**.

## Logs Examined

- **Windows Logs → Security**
- **Windows Logs → System**

The first observation was the volume of events generated by the system. My computer continuously records background activity, demonstrating why analysts need to filter and focus on relevant events.

---

# Authentication Event Observed

I found a successful authentication/logon event.

The event included useful investigation fields such as:

- Account/computer information
- Timestamp
- Logon type
- Source information
- Successful outcome

The logon event demonstrated how authentication logs can provide the information needed to investigate login activity.

The observed **Logon Type was 2**, which represents an interactive logon, generally associated with logging directly onto the local computer.

For privacy and security, sensitive identifiers were not included in this documentation.

---

# Recurring Pattern Identified

While examining the Windows System logs, I identified a recurring event.

### Event Source

**Service Control Manager**

### Event ID

**7034**

### Observation

The log indicated that the **Hola VPN Service terminated unexpectedly**.

This event appeared **3,147 times** in the System logs.

### Conclusion

This was a clear example of how repeated events can reveal persistent system behaviour or a recurring problem.

The repeated service termination does not automatically indicate malicious activity. However, the high number of occurrences would make it something worth investigating further to understand why the service repeatedly stopped unexpectedly.

This practical example reinforced the importance of learning what normal activity looks like and identifying unusual patterns.

---

# Log Retention Observed

The oldest available log entry I found was dated:

**June 13, 2026**

The investigation was performed on:

**August 30, 2026**

Based on the oldest available entry I observed, the local logs appeared to provide approximately **78 days of retention**, or around **two and a half months**.

This demonstrated an important logging lesson: if an incident occurred before the available retention period, older local evidence might no longer be available.

---

# Assessment of the Four Log Qualities

## Timestamps

The Windows logs contained timestamps, allowing events to be placed in chronological order.

## Detail

The authentication and system events contained useful information about the event, including the time, event type, source, and outcome.

## Retention

Based on the oldest entry observed, the local logs appeared to be retained for approximately 78 days.

## Integrity

Because these logs are stored locally on the machine, an attacker who gained sufficient control of the system could potentially attempt to clear or modify them.

Sending logs to protected central storage or a SIEM would provide additional protection because copies of the evidence would exist outside the compromised machine.

---

# Key Takeaways

Today's learning helped me understand that logs are the foundation underneath many security technologies and processes.

### The main lessons were:

- Logs record events that happen on systems, applications, and networks.
- Authentication, network, system, application, and audit logs answer different investigation questions.
- A useful log requires accurate timestamps, sufficient detail, retention, and integrity.
- Synchronised time using NTP is important for correlating events across systems.
- Centralised logging helps protect evidence and enables correlation.
- Analysts investigate logs by identifying patterns and filtering relevant events.
- Local logs can be valuable evidence but may be vulnerable if the machine itself is compromised.

---

# Final Reflection

Today's practical exercise made the concept of logging more real. Instead of only learning what logs are, I opened my own Windows Event Viewer, examined authentication and system events, and identified a recurring service failure pattern.

The most important lesson from today was:

> **Logs may look like ordinary records during normal operations, but during a security incident, they can become the evidence needed to reconstruct what actually happened.**

## Final Takeaway

**You can't investigate what you didn't log.**

---

**Day 38 of 90 — MyFirstHack Cybersecurity Journey**
:::writing{}

