# Day 77 — Defence in Depth

## Topic Overview

**Defence in Depth** is a cybersecurity strategy that uses multiple, overlapping security layers instead of relying on a single control. If one layer fails or is bypassed, other layers can still prevent, detect, or limit an attack.

The goal is to make compromise harder, improve the chance of detecting suspicious activity, and reduce the impact of a successful attack.

## Why One Security Control Is Not Enough

No individual security control is perfect. For example, an email filter may miss a malicious attachment, or a user may accidentally open it. Endpoint protection, application controls, network segmentation, logging, and incident response can provide additional opportunities to stop or contain the attack.

Defence in Depth assumes that individual controls can fail and plans for that possibility.

## The Swiss Cheese Model

The **Swiss Cheese Model** is a useful way to explain layered security:

- Each security layer is like a slice of cheese.
- Each slice has gaps or weaknesses.
- One layer may miss a threat, but another layer may catch it.
- Risk increases when weaknesses across several layers line up.
- Multiple independent layers make it less likely that an attacker will pass through every defence.

The model does not promise that every attack will be stopped. It illustrates why overlapping controls are stronger than depending on one control alone.

## Types of Security Layers

Defence in Depth can be organised by where a control operates and what it does.

### Layers by location

- **Physical security:** Protects buildings, devices, and equipment from unauthorised physical access.
- **Network security:** Uses firewalls, network segmentation, secure configurations, and traffic monitoring.
- **Host or endpoint security:** Uses system hardening, endpoint protection, updates, and host-based monitoring.
- **Application security:** Uses secure development, input validation, access controls, and application testing.
- **Data security:** Uses encryption, backups, permissions, and data-loss monitoring.

### Layers by function

- **Prevention:** Tries to stop an attack, such as MFA, patching, firewalls, and email filtering.
- **Detection:** Identifies suspicious activity through logs, alerts, endpoint tools, and network monitoring.
- **Response and recovery:** Helps contain an incident, remove the cause, restore systems, and learn from what happened.

People, processes, and technology all contribute. Examples include security awareness training, documented procedures, access reviews, monitoring tools, and incident-response plans.

## Examples of Defence-in-Depth Controls

| Control | How it contributes |
|---|---|
| Multi-factor authentication (MFA) | Makes account access harder with a stolen password alone. |
| Least privilege and access control | Limits what a compromised account can access or change. |
| Email filtering | Blocks or flags many malicious messages and attachments. |
| Firewalls and network segmentation | Restrict network paths and help contain movement between systems. |
| Patching and system hardening | Reduce known vulnerabilities and unnecessary exposure. |
| Endpoint protection | Can detect or block malicious files and behaviour. |
| Logging and monitoring | Help analysts identify suspicious activity and investigate events. |
| Backups and incident-response plans | Support recovery and coordinated response after an incident. |
| Security awareness training | Helps people recognise suspicious messages and report them. |

No single control guarantees protection. Controls should be selected based on the organisation's assets, risks, and environment.

## Mapping Defence in Depth to the Cyber Kill Chain

Different controls can help at different stages of an attack. This is an illustrative mapping; exact controls depend on the attack and environment.

| Attack stage | Example defensive layer |
|---|---|
| **Delivery** — a malicious file or link reaches a target | Email filtering, attachment scanning, user reporting |
| **Exploitation** — a vulnerability is used | Patching, secure configuration, application protections |
| **Installation** — malware or persistence is established | Endpoint detection, application control, monitoring for unauthorised changes |
| **Command and Control (C2)** — the compromised system communicates with an attacker | Outbound traffic controls, DNS and network monitoring, alerting on suspicious beaconing |
| **Actions on Objectives** — the attacker accesses or removes valuable data | Least privilege, data access monitoring, segmentation, data-loss controls, backups |

A defence strategy should not focus only on the perimeter. If an attacker gets inside, internal segmentation, endpoint monitoring, restricted permissions, and incident response can still reduce the damage.

## The Assume-Breach Mindset

An **assume-breach mindset** means designing security with the possibility that an attacker may get past the first line of defence. It does not mean accepting compromise as inevitable. It means preparing additional safeguards to detect, contain, and respond if prevention fails.

Useful questions include:

- If a user account is compromised, what can it access?
- Would unusual endpoint or network activity be logged and detected?
- Can a compromised device reach critical systems?
- Are backups protected and recovery procedures tested?
- Does the organisation know who will respond to an alert?

## Practical Task / Reflection

Use the following scenario to practise applying Defence in Depth. This is a learning exercise, not a claim that an incident occurred.

**Scenario:** An employee receives a phishing email and opens a malicious attachment. Assume the first control—email filtering—fails.

1. **Identify the next layer:** Name at least two other controls that might prevent or detect execution of the attachment.
2. **Limit access:** Explain how least privilege could reduce the damage if the employee's account or device is compromised.
3. **Contain movement:** Describe how network segmentation could limit access to other systems.
4. **Detect activity:** Name logs or monitoring sources that could reveal suspicious endpoint or network behaviour.
5. **Respond and recover:** Identify actions the security team should consider, such as isolating the endpoint, investigating alerts, removing the threat, and restoring from clean backups if necessary.
6. **Review the layers:** Which control failed first? Which additional layers could still help? What gaps should be addressed afterward?

### Task checklist

- [ ] Explain Defence in Depth in your own words.
- [ ] Describe the Swiss Cheese Model and why overlapping controls matter.
- [ ] Identify security layers by location and by function.
- [ ] Map at least three defensive controls to stages of an attack.
- [ ] Explain how detection, containment, and recovery help when prevention fails.
- [ ] Complete the phishing scenario reflection.

## Key Takeaways

- Defence in Depth uses multiple, overlapping security layers rather than trusting one control.
- The Swiss Cheese Model illustrates how each layer has weaknesses and how other layers can catch what one misses.
- Security layers can protect physical spaces, networks, endpoints, applications, and data.
- Prevention, detection, response, and recovery are complementary functions.
- Mapping controls to attack stages helps reveal gaps in defensive coverage.
- An assume-breach mindset encourages internal monitoring, least privilege, segmentation, and tested recovery—not just perimeter protection.
- More controls do not automatically mean better security; layers should be appropriate, maintained, monitored, and tested.

## Quick Review Questions

1. What is Defence in Depth, and why is it useful?
2. What does the Swiss Cheese Model represent?
3. How are prevention and detection different?
4. How can network segmentation limit the impact of a compromised endpoint?
5. Why should security teams plan for an attacker getting past the perimeter?

---

*MyFirstHack 90-Day Journey — Day 77*
