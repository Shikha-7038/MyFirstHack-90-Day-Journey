# Day 74 --- Threat Actors, Motivation & Capability

**MyFirstHack 90-Day Journey**\
**Day:** 74/90\
**Topic:** Who Is on the Other Side? --- Threat Actors

------------------------------------------------------------------------

## 1. Introduction

Day 74 focused on understanding **who carries out cyber attacks, why
they attack, and how their motivation and capability influence their
behaviour**.

A threat actor is a person, group, or organisation that carries out or
attempts to carry out a cyber attack.

Different attackers have different: - Motivations - Capabilities -
Targets - Techniques - Persistence - Objectives

A useful question for defenders is:

> **Who would attack us, and why?**

This connects with earlier topics: - **Day 20 --- Threat Modeling:** Who
would threaten this? - **Day 67 --- Risk:** How likely and impactful is
a threat? - **Day 71 --- Cyber Kill Chain:** How does the attack
unfold? - **Day 72 --- MITRE ATT&CK:** What techniques does the attacker
use? - **Day 73 --- Breach Analysis:** How can an attack be analysed
step by step?

------------------------------------------------------------------------

## 2. Common Threat Actor Categories

### Cybercriminals

Cybercriminals are primarily motivated by **financial gain**.

Common objectives include ransomware, financial theft, fraud, extortion,
and selling stolen information.

They often favour profitable, easier, or scalable opportunities. If a
target becomes too difficult or expensive to compromise, they may move
on.

**Motivation:** Money\
**Typical behaviour:** Opportunistic, profit-driven, scalable

### Nation-State Actors

Nation-state actors work for or are aligned with governments. They often
have significant resources and capabilities.

Common objectives include espionage, intelligence gathering, strategic
information, influence, and sabotage.

Their operations may be highly targeted, sophisticated, patient,
well-funded, and persistent. They may maintain access for months or
years when the information is valuable.

Advanced groups are often associated with **APTs (Advanced Persistent
Threats)**.

**Motivation:** Intelligence and strategic objectives\
**Typical behaviour:** Targeted, sophisticated, persistent

### Hacktivists

Hacktivists are motivated by **political or social causes**.

They may use website defacement, information leaks, disruption, or
public campaigns to draw attention to an issue or organisation they
oppose.

**Motivation:** Political or social ideology\
**Typical behaviour:** Visible disruption, leaks, defacement, public
impact

### Insiders

Insiders are employees, contractors, or other trusted users who misuse
legitimate access. The threat can also involve a legitimate account that
has been compromised or a person who is unknowingly manipulated by an
attacker.

Possible motivations include financial gain, grievance, revenge, taking
sensitive information, or sabotage.

Insiders are dangerous because they may already have access that an
external attacker would first need to obtain.

**Motivation:** Varies\
**Typical advantage:** Existing legitimate access

### Script Kiddies

"Script kiddie" is a commonly used term for attackers who rely heavily
on tools, scripts, or techniques created by others.

Their motivations can include curiosity, experimentation, mischief, or
recognition.

Their individual capability may be low, but automated tools can still
create problems.

**Motivation:** Curiosity, mischief, recognition\
**Typical behaviour:** Uses existing tools and techniques

------------------------------------------------------------------------

## 3. How Motivation Shapes Attack Behaviour

### Cybercriminal

A financially motivated attacker may find a profitable target, gain
access, achieve the financial objective, and move on. If a target
becomes too difficult, another target may offer a better return on
effort.

### Nation-State

A nation-state actor may target strategically valuable information, gain
access, remain hidden, collect intelligence, and maintain access for an
extended period.

### Hacktivist

A hacktivist may target an organisation they oppose, create visible
disruption or leaks, and publicise the action.

### Insider

An insider may steal information, damage systems, expose information, or
misuse legitimate access depending on their motivation.

The important lesson is that **motivation helps explain likely
behaviour**.

------------------------------------------------------------------------

## 4. Capability and the Realistic Threat Landscape

Threat actors exist across a broad capability spectrum.

**Lower capability** - Script kiddies - Automated attackers -
Opportunistic attackers

**Medium capability** - Organised cybercriminal groups - More capable
independent attackers

**Higher capability** - Advanced criminal groups - Nation-state teams -
Highly resourced and specialised operations

Most attacks are not highly sophisticated.

Individuals and ordinary organisations are generally more likely to
encounter: - Phishing - Automated attacks - Credential attacks -
Ransomware - Common malware - Exploitation of unpatched vulnerabilities

than a highly targeted nation-state operation.

This does not mean advanced threats should be ignored. An organisation
can still become a stepping stone, collateral target, victim of leaked
advanced tools, or target of an insider.

A balanced approach is:

> **Defend strongly against common threats while remaining aware of more
> capable threats relevant to the organisation.**

------------------------------------------------------------------------

## 5. Matching Threat Actors to Targets

### Hospital

**Most realistic threat:** Cybercriminals

Hospitals hold valuable information and depend heavily on system
availability, making ransomware and data theft attractive. Insiders can
also represent a threat.

### Defence Contractor Working on Military Technology

**Most realistic threat:** Nation-state actors / APTs

Military designs and strategic information can have significant
intelligence value. Cybercriminals remain possible, but nation-state
interest is particularly relevant.

### Controversial Oil Company

**Most realistic threat:** Hacktivists

Political or environmental disagreements may motivate attacks intended
to create public attention or disruption.

### Small Local Accounting Firm

**Most realistic threat:** Cybercriminals and opportunistic attackers

Accounting firms may hold financial and client information and can be
targeted through phishing, credential attacks, ransomware, or common
vulnerabilities.

------------------------------------------------------------------------

## 6. Cybercriminal vs Nation-State

  -----------------------------------------------------------------------
  Factor                  Cybercriminal           Nation-State
  ----------------------- ----------------------- -----------------------
  Primary motivation      Financial gain          Intelligence /
                                                  strategic objectives

  Target selection        Profitable or easier    Strategically valuable
                          targets                 targets

  If well defended        May move to an easier   May continue if
                          target                  information is valuable

  Persistence             Often focused on        May maintain access for
                          achieving the financial months or years
                          objective               

  Stealth                 Avoid detection when    Strong emphasis on
                          useful                  remaining hidden

  Resources               Vary from low to highly Often highly resourced
                          organised               

  Typical approach        Opportunistic or        Targeted and persistent
                          scalable                
  -----------------------------------------------------------------------

The key distinction is:

**Cybercriminals often optimise for profit and efficiency.**

**Nation-state actors may optimise for intelligence and strategic value,
even when greater effort and persistence are required.**

------------------------------------------------------------------------

## 7. Realistic Everyday Threats

For ordinary individuals and smaller organisations, realistic everyday
threats often include: - Phishing - Automated attacks - Weak or reused
passwords - Unpatched software - Common malware - Ransomware -
Credential theft

Basic security controls can reduce many of these risks: - Patching -
Strong passwords - MFA - Secure configurations - Security awareness -
Backups - Hardening

However, capable threats should not be completely ignored because
organisations can be targeted indirectly, advanced tools can become
widely available, and insiders can pose a threat regardless of external
attacker capability.

------------------------------------------------------------------------

## 8. Threat Modeling

Earlier threat modeling asked:

> **Who would threaten this?**

Day 74 makes that question more concrete.

Consider: - Who is the attacker? - What motivates them? - What
capability do they have? - What does the target have that they value?

A useful conceptual model is:

**Threat Actor + Motivation + Capability + Target Value → Risk**

This helps defenders focus security resources on realistic threats
rather than trying to defend equally against every imaginable attacker.

------------------------------------------------------------------------

## 9. Connecting Day 74 to the Day 73 Simulated Breach

The Day 73 scenario involved: - Researching the organisation - Targeting
finance employees - Supplier-themed phishing - A malicious attachment -
Exploitation of outdated software - A backdoor and hidden scheduled
task - Command-and-control activity - Credential theft - Lateral
movement - Access to a customer database - Exfiltration of customer
data - The stolen data eventually appearing for sale

Because the scenario was **simulated/composite**, the threat actor
cannot be definitively identified.

However, based on the behaviour and objective, a **financially motivated
cybercriminal group** would be a reasonable threat-actor hypothesis.

### Why?

The attacker: - Targeted finance employees - Used phishing to gain
access - Established persistence - Stole credentials - Moved through the
network - Accessed valuable customer data - Exfiltrated the data - Had
the stolen information appear for sale

The suspected motivation helps explain the technical behaviour: the
attacker was moving toward something they valued.

------------------------------------------------------------------------

# 10. Day 74 Task

## Step 1 --- Five Threat Actors and Motivations

  Threat Actor         Primary Motivation
  -------------------- ---------------------------------------------------
  Cybercriminals       Financial gain
  Nation-state / APT   Intelligence, strategic objectives, influence
  Hacktivists          Political or social ideology
  Insiders             Financial gain, grievance, revenge, or misuse
  Script kiddies       Curiosity, mischief, experimentation, recognition

## Step 2 --- Threat Actors and Organisations

-   **Hospital → Cybercriminals:** Valuable information and strong
    dependence on availability make ransomware and data theft realistic.
-   **Defence contractor → Nation-state/APT:** Military technology and
    strategic designs can have high intelligence value.
-   **Controversial oil company → Hacktivists:** Political or
    environmental causes can motivate visible disruption or leaks.
-   **Small local accounting firm → Cybercriminals/opportunistic
    attackers:** Financial and client information make the organisation
    attractive to common financially motivated attacks.

## Step 3 --- Cybercriminal vs Nation-State

**Cybercriminal:** Looks for profitable/easier opportunities, may
abandon a difficult target, generally has shorter objective-focused
persistence, and prefers to avoid detection while making money.

**Nation-state:** May pursue strategically valuable information despite
strong defences, can remain persistent for months or years, and places
strong emphasis on stealth.

## Step 4 --- Everyday Threat

The most realistic everyday threats for ordinary individuals and smaller
organisations are cybercriminal and automated/opportunistic attacks such
as phishing, credential attacks, ransomware, malware, and exploitation
of unpatched software.

Basic controls such as patching, MFA, strong passwords, hardening,
awareness, and backups can prevent or reduce many common attacks.

A capable threat should not be ignored because an organisation could be
targeted indirectly, advanced tools can spread, or insiders can create
risk.

## Step 5 --- Day 73 Threat Actor Analysis

A reasonable threat-actor hypothesis for the simulated Day 73 breach is
a **financially motivated cybercriminal group**.

The phishing of finance employees, persistence, credential theft,
lateral movement, customer-data theft, and eventual appearance of the
stolen data for sale all support this hypothesis.

This is an **analytical judgement based on a simulated/composite
scenario**, not confirmed attribution to a real threat actor.

------------------------------------------------------------------------

# 11. Key Takeaways

1.  A **threat actor** is the person, group, or organisation behind a
    cyber attack.
2.  Different threat actors have different motivations, including money,
    intelligence, ideology, grievance, curiosity, or strategic
    objectives.
3.  Motivation can influence target selection, techniques, persistence,
    and objectives.
4.  Threat capability ranges from low-skill automated attackers to
    highly resourced nation-state teams.
5.  Most everyday attacks are not highly sophisticated, so strong
    security fundamentals remain extremely important.
6.  Threat modeling becomes more useful when it considers realistic
    adversaries.
7.  **Motivation + capability + target value** is a useful way to think
    about threat assessment.
8.  Insiders matter because legitimate access can become a security
    risk.
9.  Nation-state threats are real but are generally concentrated around
    strategically valuable targets, while ordinary organisations are
    more likely to face common cybercrime and automated attacks.
10. Understanding the threat actor adds context to the technical attack
    and helps explain why a particular target, technique, and level of
    persistence may have been chosen.
11. The Day 73 scenario was simulated, so the cybercriminal attribution
    is a **reasonable hypothesis, not confirmed attribution**.
12. The broader progression is:

-   **Kill Chain → How the attack unfolds**
-   **ATT&CK → What techniques are used**
-   **Breach analysis → How the attack fits together**
-   **Threat actors → Who is attacking and why**

------------------------------------------------------------------------

## Final Reflection

The key shift from Day 74 is moving beyond the idea of a generic
"hacker."

An attack is carried out by a specific adversary with a particular
motivation, capability, and objective.

> **Defence is always defence against someone. Knowing who makes that
> defence more focused.**
