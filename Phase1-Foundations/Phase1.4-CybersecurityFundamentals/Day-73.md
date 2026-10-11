# Day 73 --- Kill Chain Breach Analysis

> **Portfolio Artifact:** 8 --- Kill Chain Breach Analysis\
> **Analysis Type:** Simulated/composite breach scenario\
> **Frameworks:** Cyber Kill Chain + MITRE ATT&CK concepts\
> **Scope:** Analysis of the attack scenario provided in the MyFirstHack
> Day 73 lesson\
> **Date:** 4 October 2026

------------------------------------------------------------------------

## 1. Purpose

The purpose of this analysis is to move from learning cybersecurity
frameworks to applying them to an attack scenario.

The analysis uses the **Cyber Kill Chain** to describe the attack as a
sequence of stages and uses **ATT&CK-style technique thinking** to
identify the specific methods used by the attacker.

This is a **simulated/composite scenario from the lesson**, not an
analysis of a real named breach. No real incident evidence or victim
organization was independently investigated.

------------------------------------------------------------------------

# 2. Breach Summary

A mid-sized company was targeted by an attacker who researched its
employees and used a convincing supplier-themed phishing email to
deliver a malicious attachment to finance staff.

After an employee opened the attachment, the attacker exploited outdated
software to gain code execution and establish an initial foothold. The
attacker then installed a backdoor and created a hidden scheduled task
for persistence, maintained command and control through an outbound
connection to an attacker-controlled server, explored the network, stole
credentials, moved to other systems, reached the customer database, and
copied the database to the attacker's server.

The primary objective was to **steal customer data**.

The breach was eventually discovered when the stolen information
appeared for sale.

------------------------------------------------------------------------

# 3. Source and Scope

### Source

-   MyFirstHack Day 73 lesson scenario
-   Simulated/composite breach scenario supplied as part of the lesson

### Scope

This analysis covers:

-   The attack path from reconnaissance through data theft
-   The seven stages of the Cyber Kill Chain
-   Specific attacker techniques described in the scenario
-   Defensive opportunities that could have interrupted the chain
-   A comparison of the usefulness of the Cyber Kill Chain and ATT&CK
    thinking

### Limitation

Because this is a simulated scenario, the analysis does **not**
establish what security controls the fictional company actually had or
lacked. The defensive controls below are therefore described as
**opportunities that could have broken the chain**, not as confirmed
failures.

------------------------------------------------------------------------

# 4. Stage-by-Stage Kill Chain Mapping

  ------------------------------------------------------------------------
  Kill Chain Stage        What the Attacker Did    Result
  ----------------------- ------------------------ -----------------------
  **1. Reconnaissance**   Researched the company's Collected information
                          website, employees,      for targeted social
                          email address format,    engineering
                          and finance department   

  **2. Weaponization**    Created a convincing     Prepared the delivery
                          supplier-impersonation   mechanism
                          phishing email with a    
                          malicious attachment     
                          disguised as an invoice  

  **3. Delivery**         Sent the phishing email  Malicious attachment
                          to several finance       reached potential
                          employees                victims

  **4. Exploitation**     An employee opened the   Attacker gained an
                          attachment and an        initial foothold
                          outdated software        
                          vulnerability was        
                          exploited to execute     
                          code                     

  **5. Installation**     Installed a backdoor and Persistence was
                          created a hidden         established
                          scheduled task           

  **6. Command &          Compromised machine      Attacker maintained
  Control**               connected to an          remote control
                          attacker-controlled      
                          server for remote        
                          commands                 

  **7. Actions on         Explored the network,    Customer data was
  Objectives**            stole credentials, moved stolen
                          to other systems,        
                          accessed the customer    
                          database, and copied it  
                          to the attacker's server 
  ------------------------------------------------------------------------

### Attack Path

``` text
Reconnaissance
      ↓
Weaponization
      ↓
Delivery
      ↓
Exploitation
      ↓
Installation
      ↓
Command & Control
      ↓
Actions on Objectives
      ↓
Customer Data Stolen
```

------------------------------------------------------------------------

# 5. ATT&CK-Style Technique Analysis

The Kill Chain identifies **where the attacker was in the attack**.
ATT&CK-style thinking adds the **HOW**.

  -----------------------------------------------------------------------
  Kill Chain Stage        Specific Technique /    ATT&CK Tactic
                          Attacker Method         
  ----------------------- ----------------------- -----------------------
  **Delivery**            Phishing email          Initial Access
                          containing a malicious  
                          attachment disguised as 
                          an invoice              

  **Exploitation**        Exploitation of an      Initial Access /
                          outdated software       Execution
                          vulnerability to        
                          execute code            

  **Installation**        Hidden scheduled task   Persistence
                          used to maintain access 
                          after restart           

  **Command & Control**   Outbound connection /   Command and Control
                          beaconing to an         
                          attacker-controlled     
                          server                  

  **Actions on            Credential theft        Credential Access /
  Objectives**            followed by movement to Lateral Movement
                          other systems           

  **Actions on            Copying the customer    Exfiltration
  Objectives**            database to an          
                          attacker-controlled     
                          server                  
  -----------------------------------------------------------------------

### Three clear technique-level examples

**1. Delivery --- Phishing with a malicious attachment**

The attacker impersonated a known supplier and used an invoice-themed
attachment to make the phishing email appear legitimate.

**2. Installation --- Hidden scheduled task**

The attacker created a hidden scheduled task so the malicious activity
could continue after the compromised machine restarted.

**3. Command & Control --- Beaconing**

The compromised machine established an outbound connection to an
attacker-controlled server, allowing the attacker to issue remote
commands and continue operating inside the environment.

These examples show the difference between a broad stage and a specific
attacker method:

> **Kill Chain = where the attacker is in the attack**\
> **ATT&CK = how the attacker carries out the activity**

------------------------------------------------------------------------

# 6. Where Could the Chain Have Broken?

The scenario contains several defensive opportunities where the attack
could have been interrupted.

  -----------------------------------------------------------------------
  Kill Chain Stage        Defensive Control       How It Could Break the
                                                  Chain
  ----------------------- ----------------------- -----------------------
  **Reconnaissance**      Reduce unnecessary      Limiting publicly
                          public exposure         available employee and
                                                  organizational
                                                  information could make
                                                  targeted phishing more
                                                  difficult.

  **Weaponization**       Attachment analysis and Suspicious invoice
                          sandboxing              attachments could be
                                                  analysed before being
                                                  delivered to employees.

  **Delivery**            Email filtering and     A secure email gateway
                          phishing reporting      could quarantine the
                                                  phishing message. If
                                                  delivered, employee
                                                  awareness and rapid
                                                  reporting could prevent
                                                  the attachment from
                                                  being opened.

  **Exploitation**        Patch outdated software Removing the vulnerable
                                                  software condition
                                                  could cause the
                                                  described exploit to
                                                  fail and prevent the
                                                  initial foothold.

  **Installation**        Monitor scheduled tasks An unexpected scheduled
                          and other persistence   task could be detected
                          mechanisms              and investigated before
                                                  the attacker regained
                                                  access after restart.

  **Command & Control**   Monitor outbound        An unusual connection
                          traffic and beaconing   from the compromised
                                                  host to an
                                                  attacker-controlled
                                                  server could trigger
                                                  detection and allow the
                                                  connection or host to
                                                  be contained.

  **Actions on            Monitor credential use, Suspicious access to
  Objectives**            lateral movement,       the customer database
                          sensitive database      or an unusually large
                          access, and large       outbound transfer could
                          transfers               reveal the attack
                                                  before the data was
                                                  successfully removed.
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 7. Single Most Effective Defence

## Patching the Outdated Software

For this specific scenario, the **single most effective defence** would
be keeping the vulnerable software properly patched.

The phishing email was the initial delivery mechanism, but the attacker
still needed the outdated software vulnerability to turn the opened
attachment into code execution and an initial foothold.

If the software had been patched, the attack path described in the
scenario could have stopped at the exploitation stage:

``` text
Phishing Email
      ↓
Attachment Opened
      ↓
Exploit Attempt
      ↓
PATCHED SOFTWARE
      ↓
Exploit Fails
      ↓
No Initial Foothold
      ↓
No Persistence
      ↓
No C2
      ↓
No Later Network Activity
      ↓
No Customer Database Theft
```

This does not mean patching is sufficient by itself. The scenario
demonstrates why multiple layers of defence are important. If patching
failed to stop the attack, email security, persistence monitoring, C2
detection, and data-transfer monitoring could still provide additional
opportunities to interrupt it.

------------------------------------------------------------------------

# 8. Lessons From the Analysis

## 8.1 Attacks are chains, not single events

A major breach can look like one event when viewed from the outside, but
the attack is actually made up of multiple connected activities.

In this scenario:

**Research → Phishing → Exploitation → Persistence → C2 → Network
Movement → Database Access → Data Theft**

Each successful stage enabled the attacker to move closer to the final
objective.

------------------------------------------------------------------------

## 8.2 Attackers only need one path forward, but defenders have multiple opportunities

The attacker needed to successfully progress through the chain.

The defender, however, did not need to stop the attack at every stage.
Breaking the chain at **one effective point** could prevent the later
stages from occurring.

This is why defence in depth matters.

------------------------------------------------------------------------

## 8.3 Earlier controls can prevent later investigation

Stopping the attack during delivery or exploitation is generally
preferable to discovering it only after customer data has been copied.

For example:

-   Email filtering can prevent the malicious attachment from reaching
    the user.
-   Patching can prevent exploitation.
-   Persistence monitoring can expose the attacker after initial
    compromise.
-   C2 monitoring can expose remote control activity.
-   Data-transfer monitoring can detect the final theft.

The further an attacker progresses, the more opportunities there are for
impact.

------------------------------------------------------------------------

# 9. What This Analysis Taught Me

One important lesson from this analysis is that **attacks succeed
through a sequence of dependent steps rather than one isolated action**.

Understanding an individual technique is useful, but understanding how
techniques connect across an attack makes it easier to identify where a
defender can interrupt the sequence.

The analysis also showed me that a security control does not have to
stop an attack at the beginning to be valuable. A control that detects
persistence, command and control, lateral movement, or unusual data
transfer can still break the chain before the attacker's final objective
is achieved.

------------------------------------------------------------------------

# 10. Reflection on the Analyst Perspective

This exercise was different from a hands-on technical lab because the
main task was not to configure a tool or execute commands. The focus was
on **reading an attack scenario, structuring the evidence, connecting
related security concepts, and reasoning about defensive
opportunities**.

The exercise provided practice in a way of thinking that is relevant to
SOC and threat-analysis work:

1.  Establish what happened.
2.  Break the attack into stages.
3.  Identify the techniques used.
4.  Consider what evidence or controls could expose each stage.
5.  Identify where the attack could have been interrupted.
6.  Extract lessons that can be applied to other attacks.

Rather than treating the breach as one large event, the Kill Chain made
it possible to analyse it as a sequence of smaller security problems.

------------------------------------------------------------------------

# 11. Which Framework Was More Useful?

## Cyber Kill Chain vs. ATT&CK

For this particular analysis, I found the **Cyber Kill Chain more useful
as the starting framework** because it gave me a clear structure for
reconstructing the attack from beginning to end.

It answered:

> **Where was the attacker in the attack?**

ATT&CK was more useful for adding detail after the attack path had been
established.

It answered:

> **How did the attacker perform that activity?**

The two frameworks therefore worked better together than separately:

``` text
Cyber Kill Chain
      ↓
Organises the attack into stages
      ↓
ATT&CK-style thinking
      ↓
Adds technique-level detail
      ↓
Defensive analysis
      ↓
Identify where the chain could be broken
```

For this exercise, the **Kill Chain was more useful for understanding
the overall story**, while **ATT&CK was more useful for understanding
the specific attacker behaviour**.

------------------------------------------------------------------------

# 12. Actionable Defensive Lessons

The analysis produces several practical defensive priorities:

### 1. Reduce unnecessary public exposure

Review what information about employees, departments, and organizational
structure is publicly available.

### 2. Strengthen email security

Use filtering, attachment analysis, and clear phishing-reporting
processes.

### 3. Maintain effective patch management

Prioritize vulnerabilities in software exposed to likely attack paths.

### 4. Monitor persistence mechanisms

Investigate unexpected scheduled tasks and other mechanisms that allow
software to survive restarts.

### 5. Detect unusual outbound communication

Monitor for suspicious outbound connections and beaconing from
endpoints.

### 6. Monitor identity and lateral movement

Look for unusual credential use and access between systems that normally
do not communicate.

### 7. Protect and monitor sensitive data

Monitor access to sensitive databases and investigate unusually large or
unexpected data transfers.

------------------------------------------------------------------------

# 13. Final Conclusion

This simulated breach demonstrates how a targeted attack can progress
from public reconnaissance to phishing, exploitation, persistence,
command and control, internal movement, and ultimately data theft.

The Cyber Kill Chain provided the structure needed to reconstruct the
attack. ATT&CK-style technique thinking added detail about the methods
used at individual stages.

Most importantly, the analysis showed that a breach should not only be
examined by asking **"What happened?"** A stronger analyst question is:

> **"Where could the attack have been interrupted, and what control
> could have done it?"**

That shift from describing an attack to identifying opportunities to
stop it is one of the most valuable outcomes of this exercise.

------------------------------------------------------------------------

## Key Takeaways

-   The Cyber Kill Chain helps reconstruct an attack from **beginning to
    objective**.
-   ATT&CK adds **technique-level detail** about how attackers perform
    activities.
-   Phishing, exploitation, scheduled-task persistence, C2 beaconing,
    credential theft, lateral movement, and data theft can form one
    connected attack path.
-   A defender does not need to stop every stage; **breaking one
    critical link can stop the progression**.
-   Patching vulnerable software could have prevented the initial
    foothold in this scenario.
-   Detection at later stages remains valuable if earlier controls fail.
-   Good attack analysis connects **attacker behaviour → defensive
    opportunities → actionable lessons**.
-   This exercise demonstrates analytical thinking that complements
    hands-on cybersecurity work.
