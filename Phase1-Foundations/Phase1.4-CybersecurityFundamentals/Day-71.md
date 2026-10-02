# Day 71 --- Cyber Kill Chain

## Topic: Trace an Attack Through the Chain

The Cyber Kill Chain is a framework for understanding a cyberattack as a
sequence of stages rather than as one isolated event. A serious attack
may develop over hours, days, weeks, or months, and each stage gives
defenders an opportunity to detect, disrupt, or contain the attack.

## The Seven Stages

1.  **Reconnaissance** --- The attacker researches the target and
    collects useful information.
2.  **Weaponization** --- The attacker prepares a malicious tool, file,
    exploit, or payload.
3.  **Delivery** --- The attacker gets the malicious content to the
    target.
4.  **Exploitation** --- The attacker uses a weakness or interaction to
    gain access or execute code.
5.  **Installation** --- The attacker establishes persistence so access
    can survive disruptions such as a reboot.
6.  **Command and Control (C2)** --- The compromised system communicates
    with the attacker for instructions or remote control.
7.  **Actions on Objectives** --- The attacker carries out the final
    goal, such as stealing data, spying, encrypting files, or causing
    damage.

**Simple progression:** Research → Build → Deliver → Exploit → Persist →
Control → Act

## 1. Reconnaissance

The attacker researches the target. Information can include employee
names, email addresses, organization structure, technologies, public
systems, and potential weaknesses.

**Mental model:** "What can I learn about the target?"

**Connection:** Day 26 --- Footprinting.

## 2. Weaponization

The attacker prepares the components needed for the attack, such as a
malicious document, payload, exploit, script, or malware.

**Mental model:** "How can I turn what I learned into an attack?"

## 3. Delivery

The attacker gets the malicious weapon to the target through methods
such as phishing emails, malicious attachments, malicious links, or
compromised websites.

**Mental model:** "How do I get the attack to the target?"

## 4. Exploitation

The attacker uses a weakness to gain access or execute code. This can
involve vulnerable software, misconfiguration, security weaknesses, or
user interaction.

**Mental model:** "How can I use a weakness to get in?"

**Connection:** Day 67 --- Threat, Vulnerability and Risk.

## 5. Installation

The attacker establishes persistence so they can maintain access.
Examples include malware, backdoors, rogue accounts, scheduled tasks,
and cron jobs.

**Mental model:** "How do I make sure I don't lose my foothold?"

**Connection:** Day 62 --- Persistence.

## 6. Command and Control

A compromised system may communicate with an attacker-controlled server
to receive instructions, send information, or maintain remote control.
Beaconing or "phoning home" is one concept associated with this stage.

**Mental model:** "How do I control the compromised system remotely?"

**Connection:** Day 58 --- Beaconing / Phoning Home.

## 7. Actions on Objectives

The attacker performs the final objective, such as stealing sensitive
information, encrypting files for ransom, spying, moving deeper into a
network, sabotaging systems, or manipulating information.

**Mental model:** "What does the attacker actually want to accomplish?"

**Connection:** Day 66 --- CIA Triad. Attacker objectives can affect
confidentiality, integrity, and availability.

# Breaking the Chain

Defenders can attempt to interrupt an attack at different stages.
Examples include: **Delivery:** email security or spam filters can block
malicious messages. **Exploitation:** patching and secure configuration
can reduce exploitable weaknesses. **Installation:** persistence
monitoring can detect unexpected scheduled tasks or rogue accounts.
**Command and Control:** network monitoring can identify suspicious
outbound communication or beaconing. **Actions on Objectives:** access
controls, data protection, and monitoring can help detect or limit data
theft or other harmful actions.

## Defence in Depth

The Kill Chain connects closely with defence in depth. Multiple layers
of security create multiple opportunities to detect or disrupt an
attacker. For example: **Email filtering → Endpoint protection →
Patching → Persistence monitoring → Network monitoring → Data
protection.** If one control fails, another may still detect the
attacker later.

## Earlier Detection

Stopping an attack earlier generally gives defenders more opportunity to
limit damage. Blocking a malicious email is generally preferable to
discovering the attacker after persistence or data theft has occurred.
Later detection still matters because it can help contain the incident
and prevent further damage.

# The Kill Chain as a Detection Tool

-   **Reconnaissance:** unusual scanning, probing, or suspicious
    information gathering.
-   **Delivery:** phishing emails, suspicious attachments, or malicious
    links.
-   **Exploitation:** unexpected code execution or exploitation
    attempts.
-   **Installation:** new persistence mechanisms, scheduled tasks, rogue
    accounts, or suspicious startup changes.
-   **C2:** unusual outbound connections, beaconing, or suspicious
    external destinations.
-   **Actions on Objectives:** large data transfers, unusual access to
    sensitive information, mass file encryption, or other activity
    consistent with the attacker's goal.

# The Kill Chain in Incident Response and Analysis

Knowing the stage can help a security team understand what may have
happened, what could happen next, how urgent the situation may be, and
what defensive actions should be considered. After an incident, evidence
can be mapped to reconnaissance, delivery/exploitation, installation,
C2, and actions on objectives to reconstruct the attacker's path. This
connects with Day 65 Linux forensics, where processes, connections,
logs, accounts, persistence, and other evidence were used to reconstruct
an incident.

# Seeing Attacks as Processes

An event is something that happens; a process develops through stages.
The Kill Chain encourages defenders to think of attacks as processes
that can be observed and interrupted.

-   **Detection:** Where should I look for signs of the attack?
-   **Prevention:** Which stage can I block?
-   **Response:** Where is the attacker now, and what should happen
    next?
-   **Analysis:** How did the attacker move through the stages?

# Connecting the Kill Chain to Previous Learning

  -----------------------------------------------------------------------
  Kill Chain stage                    Earlier learning
  ----------------------------------- -----------------------------------
  Reconnaissance                      Day 26 --- Footprinting

  Weaponization                       Days 56/61 --- Malicious scripts
                                      and attack preparation

  Delivery                            Phishing and social engineering
                                      concepts

  Exploitation                        Day 67 --- Threat, Vulnerability
                                      and Risk

  Installation                        Day 62 --- Persistence

  Command & Control                   Day 58 --- Beaconing / Phoning Home

  Actions on Objectives               Day 66 --- CIA Triad
  -----------------------------------------------------------------------

# The Kill Chain Is a Model

The seven stages are not a rigid checklist that every real-world attack
follows perfectly. Real attacks can skip, repeat, overlap, or branch
across stages. The Kill Chain is best understood as a thinking and
analysis framework for identifying opportunities to detect, disrupt, and
contain attack progression.

# Day 71 Task --- Trace an Attack Through the Chain

## Step 1: Seven Stages in My Own Words

1.  Reconnaissance --- research the target.
2.  Weaponization --- prepare the malicious tool or payload.
3.  Delivery --- get the weapon to the target.
4.  Exploitation --- use a weakness to gain access or execute code.
5.  Installation --- establish persistence.
6.  Command and Control --- communicate with the compromised system.
7.  Actions on Objectives --- achieve the attacker's final goal.

## Step 2: Scenario Mapping

  -----------------------------------------------------------------------
  Scenario event          Stage                   Reason
  ----------------------- ----------------------- -----------------------
  Browse company LinkedIn Reconnaissance          Collecting information
  for employee names and                          about the target.
  email formats                                   

  Craft malicious Word    Weaponization           Preparing the malicious
  document with a fake                            weapon.
  invoice                                         

  Email it to an          Delivery                Getting the weapon to
  accountant                                      the target.

  Accountant opens it and Exploitation            Using the
  hidden code runs                                interaction/weakness to
                                                  execute code and gain
                                                  access.

  Create hidden scheduled Installation            Establishing
  task                                            persistence.

  Malware connects to     Command and Control     The compromised system
  attacker server                                 communicates with the
                                                  attacker.

  Locate and steal        Actions on Objectives   Carrying out the final
  customer database                               objective.
  -----------------------------------------------------------------------

## Step 3: Three Places to Break the Chain

### Early --- Delivery

**Defence:** Spam/phishing filtering.

**How it stops the attack:** The malicious email can be blocked before
it reaches the accountant, preventing the attack from progressing to
exploitation.

### Middle --- Installation

**Defence:** Persistence detection.

**How it stops the attack:** Monitoring can identify suspicious
scheduled tasks or other persistence mechanisms, helping remove the
attacker's ability to maintain access.

### Late --- Command and Control

**Defence:** Beaconing/C2 detection.

**How it stops the attack:** Suspicious outbound communication can be
detected and blocked, disrupting remote attacker control.

## Step 4: Connections to Earlier Lessons

-   **Reconnaissance → Day 26 Footprinting:** collecting information
    about a target and its visible attack surface.
-   **Installation → Day 62 Persistence:** rogue accounts, cron jobs,
    scheduled tasks, and other mechanisms can maintain access.
-   **Command and Control → Day 58 Beaconing / Phoning Home:**
    compromised systems may communicate with an external server for
    instructions or information exchange.

## Step 5: Defender's Advantage

The attacker needs to successfully progress through multiple stages to
reach the objective. The defender does not necessarily need to stop
every stage; interrupting the progression at an important point can
prevent or limit the attack.

**The attacker has to keep succeeding. The defender only needs to
successfully interrupt the attack at an important point.**

Breaking the chain earlier is generally better because the attacker has
had less opportunity to establish access, persistence, control, or cause
damage. For example, blocking a malicious email is generally cleaner
than discovering the attack after customer data has already been stolen.
Later detection remains valuable because it can still contain the
incident, limit further damage, and provide evidence for investigation.

# Key Takeaways --- Day 71

1.  **A cyberattack is a process:** serious attacks often progress
    through multiple stages rather than being one isolated event.
2.  **Every stage is a defensive opportunity:** defenders can detect,
    block, disrupt, or contain attacks at multiple points.
3.  **The attacker must keep succeeding:** reaching the final objective
    requires progression through the attack.
4.  **Earlier detection can reduce damage:** stopping an attack sooner
    generally limits access and potential impact.
5.  **Defence in depth creates multiple opportunities:** layered
    controls reduce reliance on one defensive mechanism.
6.  **The Kill Chain connects previous learning:** footprinting,
    vulnerabilities, persistence, beaconing, CIA, monitoring, and
    forensics can be viewed as parts of one attack story.
7.  **The Kill Chain is a model:** real attacks can skip, repeat,
    overlap, or branch across stages.

# Final Mental Model

**Reconnaissance → Weaponization → Delivery → Exploitation →
Installation → Command & Control → Actions on Objectives**

Instead of only asking, **"Did an attack happen?"**, ask: **"Where is
the attacker in the process, and where can we interrupt the
progression?"**

**Day 71 complete. 🔐**
