# Day 82 — Open-Source Intelligence (OSINT)

## 1. What Is OSINT?

**OSINT (Open-Source Intelligence)** is the process of collecting, analysing, and interpreting information from publicly available sources to understand a person, organisation, or potential target.

The term *open-source* means that the information is openly available; it does not necessarily refer to open-source software.

OSINT turns separate pieces of public information into useful intelligence. In cybersecurity, it can support reconnaissance, threat intelligence, exposure assessment, and defensive decision-making.

## 2. Common Sources of OSINT

OSINT may draw on sources such as:

- **Search engines:** Public webpages, indexed profiles, articles, and mentions.
- **Social media:** Public posts, profile details, interests, professional information, and visible connections.
- **Professional platforms:** Public information about job roles, education, skills, and organisational relationships.
- **Company websites:** Business activities, services, teams, and other published information.
- **Public documents:** Reports, presentations, and documents made available online.
- **Public records:** Information legally accessible to the public, depending on the jurisdiction and record type.

Information from these sources may appear harmless individually. When combined, it can reveal a more detailed picture of a person or organisation.

## 3. The OSINT Process

### Step 1: Collect information

Gather relevant information from publicly available sources with a clear objective and within legal and ethical boundaries.

### Step 2: Analyse information

Examine the collected material for patterns, relationships, and useful details. The goal is to understand what the information reveals collectively, rather than treating every item in isolation.

### Step 3: Identify risks or opportunities

Analysis may reveal public exposure, organisational relationships, potential security weaknesses, or information that could be misused. A public clue alone does not prove that a system is vulnerable; further authorised verification may be required.

### Step 4: Apply the findings

Use the resulting intelligence to support decisions. Defenders may reduce unnecessary exposure, improve awareness, investigate threats, or strengthen security controls.

**Process summary:** Collect → Analyse → Identify Risks → Defend

## 4. How Attackers Use OSINT

Attackers may use OSINT during **reconnaissance**, the stage in which they gather information about a potential target before attempting an attack.

### Targeted phishing

Public details about a person's role, interests, or organisation can help an attacker tailor a convincing phishing message.

### Social engineering

Social engineering involves manipulating people into revealing information or taking actions that compromise security. Familiar details can make a fraudulent request seem trustworthy.

### Impersonation

Information about employees, organisations, or professional relationships may help an attacker pretend to be a trusted individual or legitimate organisation.

### Identifying possible entry points

Public information about an organisation's services, technologies, or structure may help attackers decide which areas to investigate further. OSINT alone does not establish that a weakness exists.

## 5. How Defenders Use OSINT

OSINT can support legitimate defensive security work in several ways.

### Assessing public exposure

Individuals and organisations can review what information is publicly available and determine whether unnecessary details should be removed or restricted.

### Supporting threat intelligence

Security teams can use relevant public information to understand potential threats, attacker activity, and risks affecting their organisation.

### Improving security awareness

Understanding how attackers gather information helps people recognise that a message containing accurate personal or professional details may still be fraudulent.

### Strengthening security controls

Findings can inform privacy improvements, exposure reduction, and the prioritisation of appropriate security measures.

### Reviewing an organisation's digital footprint

Security teams can examine publicly visible organisational information to identify unintended exposure and decide whether additional safeguards are needed.

## 6. OSINT and the Cyber Kill Chain

OSINT can support the **reconnaissance** stage of the Cyber Kill Chain. During reconnaissance, an attacker gathers information about a potential target. That information may inform later activities, such as delivering a phishing message or investigating a possible weakness.

OSINT is not limited to one stage. Public information can also help defenders investigate threats and understand how an attack may have been planned.

## 7. OSINT and Spear-Phishing

**Spear-phishing** is a targeted form of phishing in which a message is tailored to a particular person or organisation rather than sent indiscriminately to many recipients.

OSINT can make spear-phishing more convincing by providing details that help personalise a message.

For example:

1. An attacker finds public information about an organisation, its employees, or its services.
2. The attacker identifies a relevant role or business relationship.
3. The attacker creates a message that appears connected to the recipient's work.
4. The recipient may be more likely to trust the message because it contains familiar details.

The information may be accurate, but that does not prove the sender is genuine. Unexpected requests should be verified through independent, trusted channels, especially when they ask for credentials, payments, sensitive information, or urgent action.

## 8. Self-OSINT and Digital Footprint Management

**Self-OSINT** means examining one's own publicly discoverable information to understand what others might learn. It can help people assess their digital footprint and manage exposure.

Common defensive measures include:

- Reviewing social media privacy settings.
- Avoiding unnecessary disclosure of location, routines, and sensitive personal details.
- Checking whether an email address appears in known data breaches using a reputable service.
- Changing exposed passwords and avoiding password reuse.
- Closing unused accounts where appropriate.
- Reviewing public profiles, photos, and documents for unnecessary information.
- Enabling multi-factor authentication (MFA) wherever available.

Not all information can be removed. Public records, historical breaches, and posts shared by other people may remain accessible. Awareness and appropriate security practices help manage the remaining risk.

## 9. OSINT: Attacker and Defender Perspectives

| Attacker perspective | Defender perspective |
|---|---|
| Gather information about a target. | Understand public exposure. |
| Combine details to personalise attacks. | Identify and reduce unnecessary exposure. |
| Use information to support phishing or impersonation. | Improve awareness and verification practices. |
| Look for possible weaknesses or entry points. | Assess exposure and strengthen security controls. |

The techniques used to collect and analyse public information can serve different purposes. Authorisation, intent, and how the findings are used are important in distinguishing responsible security work from harmful activity.

## 10. Ethical and Responsible OSINT

OSINT should be conducted within legal, ethical, and privacy boundaries.

Responsible practice includes:

- Using publicly available information appropriately.
- Respecting privacy and applicable laws.
- Investigating only authorised targets.
- Avoiding unauthorised access to private accounts or systems.
- Protecting collected information from unnecessary disclosure.
- Verifying information before treating it as accurate.

Public availability does not automatically mean information is reliable, current, or appropriate for every use. Analysts should consider context, source quality, and uncertainty.

## Key Takeaways

- **OSINT** turns publicly available information into useful intelligence through collection and analysis.
- Common sources include search engines, social media, professional platforms, company websites, public documents, and public records.
- The process involves collecting information, analysing connections, identifying risks, and applying findings.
- Attackers may use OSINT to support reconnaissance, targeted phishing, social engineering, impersonation, and the identification of possible entry points.
- Defenders use OSINT to understand exposure, support threat intelligence, improve security awareness, and strengthen controls.
- Accurate personal or professional details in a message do not prove that the sender is trustworthy.
- A public clue is not proof of a vulnerability; findings should be verified appropriately.
- Self-OSINT can help manage digital exposure through privacy reviews, password hygiene, account maintenance, and MFA.
- OSINT should be conducted legally, ethically, and with respect for privacy.
