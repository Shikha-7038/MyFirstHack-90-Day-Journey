# MyFirstHack — Day 81: Incident Response

## Topic Overview

Incident response is the structured process an organization follows to identify, manage, contain, and recover from cybersecurity incidents. It helps limit damage, preserve relevant evidence, restore services safely, and improve future security.

Examples of security incidents include unauthorized access, data breaches, malware infections, and ransomware incidents.

## The Six Phases of Incident Response

### 1. Preparation
Preparation gets the organization ready before an incident occurs.

- Create an incident response plan and assign responsibilities.
- Train the response team and prepare appropriate tools.
- Harden systems by applying patches, removing weaknesses, and implementing security controls.
- Maintain protected, tested backups and communication procedures.
- Use an assume-breach mindset: prepare for the possibility that preventive controls may fail.

**Purpose:** Be ready to detect, manage, and recover from an incident.

### 2. Identification
Identification involves detecting suspicious activity, confirming whether an incident has occurred, and assessing its scope and severity.

- Review relevant logs, security alerts, and unusual activity.
- Investigate processes, file changes, and network connections.
- Determine which systems may be affected and whether the incident has spread.
- Record relevant evidence and build an initial understanding of what happened.

**Purpose:** Understand the incident, its likely cause, and its impact.

### 3. Containment
Containment limits damage and helps prevent an incident from spreading.

- Isolate affected systems or restrict suspicious connections.
- Limit access to affected accounts, systems, or resources where necessary.
- Use network segmentation to reduce communication between network zones.
- Consider connected systems and shared resources that may also be at risk.
- Preserve relevant evidence where feasible; avoid destructive actions such as wiping a system prematurely.

**Purpose:** Stop or limit further damage while managing operational impact.

**Segmentation vs. isolation:** Segmentation divides a network into zones and controls traffic between them. Isolation restricts an affected system's communication or access to other systems.

### 4. Eradication
Eradication removes the threat and addresses the weaknesses that allowed the incident.

- Remove malware and other malicious components.
- Investigate and remove persistence mechanisms.
- Check for unauthorized accounts or other malicious changes.
- Fix exploited vulnerabilities and misconfigurations.
- Check whether other systems may also be compromised.

A **persistence mechanism** is a method an attacker uses to maintain or regain access to a compromised system. Examples can include unauthorized accounts or malicious scheduled tasks.

**Purpose:** Remove the threat and the attacker's identified ways of maintaining access.

### 5. Recovery
Recovery restores affected systems and services to safe, normal operation.

- Restore clean data from protected backups or rebuild systems when necessary.
- Apply security updates and verify system integrity.
- Test restored data and services for correct operation.
- Reconnect systems when appropriate after security checks.
- Monitor for signs of renewed malicious activity.

Backups should be protected and tested before an incident occurs. Recovery is not simply turning systems back on; security and functionality must both be verified.

**Purpose:** Restore services and data safely and monitor for renewed activity.

### 6. Lessons Learned
Lessons Learned reviews the incident and the response to improve future security.

- Review how the incident began and how it spread.
- Identify which controls and response actions worked well and which did not.
- Assess detection, containment, evidence handling, backups, and communication.
- Document gaps and assign improvements to responsible people.
- Update security controls, monitoring, training, backups, and response plans.

**Purpose:** Improve future prevention, detection, response, and recovery.

## Why a Structured Process Matters

A structured process helps a team prioritize actions, coordinate responsibilities, and avoid overlooking important parts of an incident. Panic can lead to mistakes such as wiping a system before preserving evidence, delaying containment, missing other compromised systems, or restoring services before the threat has been addressed.

Incident response requires timely, coordinated decisions that balance damage limitation, evidence preservation, business availability, and safe recovery.

## Applying the Phases to a Hypothetical Ransomware Incident

**Scenario:** A company's file server becomes inaccessible, and files appear to have been encrypted.

1. **Preparation:** The company has a response plan, assigned roles, security controls, and protected backups that have been tested.
2. **Identification:** The team investigates reports, alerts, logs, file activity, and network connections to confirm the incident and assess its scope.
3. **Containment:** The team isolates affected systems or restricts their communication and checks whether connected systems or shared resources are also at risk. Relevant evidence is preserved where feasible.
4. **Eradication:** The team investigates the entry point, removes malicious components, checks for persistence, fixes exploited weaknesses, and checks for other compromised systems.
5. **Recovery:** The team restores clean data, verifies security and functionality, and monitors systems before and after returning them to service.
6. **Lessons Learned:** The organization reviews the incident and response, documents findings, and improves its controls and response plan.

Restoring encrypted files alone does not resolve the entire incident. The organization must also investigate the cause, address unauthorized access, and verify that restored systems are safe.

## Three Important Incident Response Trade-offs

### Speed vs. Evidence
Acting quickly can limit damage, but wiping an affected system too soon may destroy valuable evidence. The team should contain the threat promptly while preserving relevant evidence wherever feasible.

### Containment vs. Availability
Isolating an affected system can prevent further spread, but it may interrupt essential business services. The team should limit the threat while keeping critical services running safely wherever possible.

### Eradication vs. Recovery Speed
Restoring systems before fully addressing the threat could allow the attacker to regain access. The team should verify that the threat has been addressed before safely returning systems to normal operation.

## Connections to Earlier MyFirstHack Topics

- **Response planning, hardening, and assume-breach:** Support preparation and readiness.
- **Logs, processes, and network connections:** Support identification and investigation.
- **Network segmentation and isolation:** Help contain an incident and limit spread.
- **Persistence mechanisms and vulnerability management:** Help remove attacker access and address the cause of compromise.
- **Backups and availability:** Support safe recovery of data and services.
- **Cyber Kill Chain and breach analysis:** Help organize the attack and identify improvements during the review.

## Task / Exercise — Day 81

Use the following prompts to practice incident response thinking. The scenario is hypothetical; these prompts do not imply that a real incident was handled.

1. **Name the six phases in order.** Explain the purpose of each phase in your own words.
2. **Explain why process beats panic.** Describe mistakes that can happen when a team reacts without a structured plan.
3. **Walk through a ransomware scenario.** Explain what the team should consider during each of the six phases.
4. **Reason through one tension.** Choose one trade-off and explain how the team can balance the competing priorities:
   - Speed vs. evidence preservation
   - Containment vs. business availability
   - Complete eradication vs. rapid recovery
5. **Connect the phases to earlier topics.** Relate each phase to relevant MyFirstHack concepts and explain the connection.

## Key Takeaways

- Incident response follows six phases: Preparation, Identification, Containment, Eradication, Recovery, and Lessons Learned.
- Identification establishes what happened and assesses the incident's scope; containment limits further damage.
- Eradication removes the threat and addresses the weaknesses that enabled the incident; recovery restores and verifies safe operation.
- Evidence should be preserved wherever feasible, but evidence collection should not cause dangerous delays in containing an active threat.
- Isolating systems can affect business availability, so response decisions should account for operational needs and security.
- Backups need protection and testing, and restored systems should be checked before normal operation resumes.
- Lessons Learned should identify what worked as well as what needs improvement.
- Incident response is not only about restoring operations; it is also about understanding the incident and improving future readiness.
