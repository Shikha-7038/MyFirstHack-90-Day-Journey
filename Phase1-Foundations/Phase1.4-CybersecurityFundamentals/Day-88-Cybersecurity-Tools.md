# Day 88 — Cybersecurity Tools: Mapping the Security Toolbox

## Overview

Cybersecurity teams use tools to detect suspicious activity, prevent attacks, investigate incidents, and manage security over time. Each tool category supports a particular kind of work. Products may differ in interface, features, and workflow, but understanding the category gives a foundation for learning specific tools.

## 1. Detection Tools

Detection tools help security teams identify suspicious activity and potential threats.

### SIEM — Security Information and Event Management
- Collects and centralises logs from servers, endpoints, network devices, and applications.
- Supports searching, filtering, correlating events, and generating alerts.
- Example use: investigating repeated failed logins followed by a successful login.
- Related learning: log analysis, event correlation, and SOC monitoring.

### EDR — Endpoint Detection and Response
- Monitors individual endpoints such as laptops, desktops, and servers.
- Observes processes, connections, and suspicious behaviour.
- Helps analysts investigate endpoint threats and may support response actions such as isolating a device.
- Example use: investigating an unfamiliar program that creates a persistence mechanism and contacts an external server.

### IDS/IPS — Intrusion Detection/Prevention System
- Inspects network traffic for signs of suspicious or malicious activity.
- **IDS** detects and alerts; **IPS** can block traffic that matches configured rules.
- Example use: alerting on or blocking traffic that matches a known attack pattern.

### Network Monitoring
- Tracks network traffic, flows, connections, and anomalies.
- Can help identify unusual outbound communication and command-and-control beaconing.
- Example use: investigating a workstation that repeatedly contacts an unfamiliar external address.

| Detection category | Main focus |
|---|---|
| SIEM | Logs and events from multiple sources |
| EDR | Activity on individual endpoints |
| IDS/IPS | Network traffic and potential attacks |
| Network monitoring | Traffic patterns, flows, and anomalies |

## 2. Prevention Tools

Prevention tools enforce controls intended to stop attacks or reduce their likelihood and impact.

### Firewalls
- Allow or block network traffic according to configured rules.
- Help restrict access to services and segment networks.
- Example: blocking inbound connections to a service that should not be publicly accessible.

### Secure Email Gateways
- Filter suspected phishing emails and malicious attachments or links.
- Apply email security policies and quarantine suspicious messages.
- Example: quarantining a supplier-impersonation email with a suspicious invoice attachment.

### IAM — Identity and Access Management
- Manages user identities, authentication, and access permissions.
- Supports least privilege, role-based access, and multi-factor authentication (MFA).
- Example: allowing an employee to access a finance application without granting administrative privileges.

### Endpoint Protection
- Helps prevent or detect malicious software on computers and servers.
- Includes traditional antivirus and may overlap with EDR capabilities.
- Example: blocking a file identified as malicious before it executes.

## 3. Investigation Tools

Investigation tools help analysts understand what happened, how it happened, and what systems or data may have been affected.

### Packet Analysers
- Capture or inspect network packets and communication details.
- Help examine addresses, protocols, connections, and unusual traffic.
- Example tool: **Wireshark**.

### Digital Forensics Tools
- Examine systems, storage, files, and digital artefacts while preserving evidence.
- Help reconstruct activity and investigate possible compromise.
- Investigators should document their steps and protect evidence integrity.

### Sandboxes
- Run suspicious files or programs in an isolated environment to observe their behaviour.
- Can reveal file changes, process activity, and attempted network connections.
- A sandbox reduces risk but does not guarantee safety; some malware can detect or evade analysis environments.

### Threat Intelligence Platforms
- Organise information about threats, attacker techniques, campaigns, and indicators of compromise.
- Help provide context during investigations and threat hunting.
- **MITRE ATT&CK** is a knowledge base of adversary tactics and techniques that supports consistent descriptions of attacker behaviour; it is often used alongside security tools and threat intelligence.

## 4. Management Tools

Management tools help organisations maintain security controls, address weaknesses, and track risk over time.

### Vulnerability Scanners
- Assess systems for known vulnerabilities and other weaknesses.
- May associate findings with relevant **CVE** identifiers.
- Findings should be checked for accuracy, applicability, and risk before prioritising remediation.

### Patch Management Tools
- Help plan, deploy, and track software updates and security fixes across systems.
- Identify devices that remain unpatched and support update schedules.
- Example: deploying an approved security update to vulnerable workstations and checking deployment status.

### GRC Platforms — Governance, Risk, and Compliance
- Help document security controls, risks, compliance requirements, and audit evidence.
- Support risk tracking, control mapping, and compliance reporting.
- Example: recording a requirement, the control used to address it, and evidence that the control is operating.

## 5. How the Four Activities Work Together

Consider a hypothetical incident involving a suspicious email attachment:

1. **Prevention:** A secure email gateway attempts to filter the message.
2. **Detection:** If suspicious activity occurs, EDR may identify unusual endpoint behaviour while the SIEM correlates relevant logs and alerts.
3. **Investigation:** Analysts examine endpoint evidence, network traffic, and threat intelligence to understand what happened.
4. **Management:** The organisation addresses underlying weaknesses, updates controls, and records follow-up actions.

These activities are connected, but they do not always happen in a strict sequence. Teams may use them together and revisit earlier steps as new evidence appears.

## 6. Tools and Cybersecurity Roles

| Role | Common tool categories | Typical use |
|---|---|---|
| SOC Analyst | SIEM, EDR, network monitoring | Monitor alerts and investigate suspicious activity |
| Incident Responder | EDR, digital forensics tools | Determine incident scope, support containment and recovery, and gather evidence |
| Penetration Tester | Vulnerability scanners, packet analysers, specialised testing tools | Conduct authorised testing to identify and validate weaknesses |
| GRC Analyst | GRC platforms, vulnerability management tools | Track risks, controls, compliance requirements, and evidence |

Tool usage varies by organisation and job responsibilities. Penetration testing must always stay within an authorised scope.

## 7. Tools Change; the Thinking Endures

Specific products can be renamed, replaced, or updated, while the underlying purpose of a category often remains similar. For example:

- Understanding log analysis helps when learning different SIEM platforms.
- Understanding endpoint behaviour helps when learning different EDR products.
- Understanding vulnerabilities helps when interpreting results from different scanners.
- Understanding network protocols helps when analysing traffic with different tools.

Products are not identical: their capabilities, interfaces, query languages, integrations, and workflows can differ. Category knowledge provides a foundation, while practical experience helps demonstrate that knowledge.

When encountering an unfamiliar tool, ask:
1. What security problem does it address?
2. What data or evidence does it provide?
3. How can that information support an investigation or security decision?

## 8. Day 88 Task — Map the Security Toolbox

### Step 1: State the central point

Security tools may have different names and interfaces, but tools in the same category generally serve similar purposes. Understanding what evidence to look for, how to interpret it, and what action to take transfers between products. I do not need to have used every product in an entry-level job description, but I should understand the category and practise with relevant tools where possible.

### Step 2: Name the detection categories

- **SIEM:** Centralises logs, supports searching and correlation, and generates alerts; supports log analysis and SOC monitoring.
- **EDR:** Watches individual endpoints for suspicious behaviour; supports endpoint investigation and response.
- **IDS/IPS:** Inspects network traffic for attack indicators; IDS alerts and IPS can block traffic.
- **Network monitoring:** Tracks traffic and flows to identify anomalies such as beaconing.

### Step 3: Name the other category groups

**Prevention**
- **Firewalls:** Control permitted network traffic.
- **IAM/MFA:** Manage access and strengthen authentication.

**Investigation**
- **Packet analysers:** Examine network packets and communication.
- **Digital forensics tools:** Examine compromised systems and preserve evidence.

**Management**
- **Vulnerability scanners:** Identify known weaknesses.
- **Patch management tools:** Coordinate software updates and security fixes.

### Step 4: Map tools to roles

- **SOC Analyst:** SIEM and EDR — monitor alerts and investigate suspicious activity.
- **Incident Responder:** EDR and digital forensics — investigate affected systems and gather evidence.
- **Penetration Tester:** Vulnerability scanners and packet analysers — conduct authorised testing and examine traffic.
- **GRC Analyst:** GRC platforms and vulnerability management tools — track risks, controls, and compliance evidence.

### Step 5: Translate into interview confidence

If a job description lists a product I have not used, I can explain the category's purpose and the underlying work honestly. For example:

> “I understand that a SIEM collects and centralises logs, supports searching and correlation, and helps analysts identify suspicious activity. I haven't used this specific product yet, but I understand the purpose of SIEM tools and am building practical log-analysis skills. I would need to learn its particular interface and query language.”

This shows understanding without claiming experience I do not have. Employers vary: some train junior candidates on their tools, while others expect hands-on experience with specific products.

## 9. Key Takeaways

- Cybersecurity tools support four connected activities: **detection, prevention, investigation, and management**.
- SIEM, EDR, IDS/IPS, and network monitoring have different but complementary views of suspicious activity.
- Firewalls, secure email gateways, IAM, and endpoint protection help enforce preventive controls.
- Packet analysers, forensic tools, sandboxes, and threat intelligence support deeper investigation.
- Vulnerability scanners, patch management tools, and GRC platforms help maintain security over time.
- Different roles use different combinations of tools; responsibilities and product choices vary by organisation.
- Tools within a category are not identical, but understanding the category and the security reasoning makes learning a new product easier.
- Be honest about practical experience in interviews and support your knowledge with hands-on practice.
