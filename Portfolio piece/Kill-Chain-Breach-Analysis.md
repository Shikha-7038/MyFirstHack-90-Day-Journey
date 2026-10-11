============================================================ KILL CHAIN
BREACH ANALYSIS
============================================================

Analyst: Shikha Date: 4 October 2026 Subject: Simulated Customer Data
Breach Source: MyFirstHack Day 73 lesson scenario (simulated/composite
scenario)

  --------------------
   1\. BREACH SUMMARY
  --------------------

A mid-sized company was targeted by an attacker who researched the
organisation and its employees before sending a convincing
supplier-themed phishing email to finance staff. The attacker exploited
outdated software, established persistence, maintained command and
control, moved through the network, and accessed the customer database.

The attacker's goal was to steal customer data, and the objective was
achieved when the customer database was copied to the
attacker-controlled server. The breach was discovered later when the
stolen data appeared for sale.

  ------------------------
   2\. KILL CHAIN MAPPING
  ------------------------

RECONNAISSANCE: The attacker researched the company's website,
employees, professional networks, email address format, and finance
department names.

WEAPONIZATION: The attacker created a convincing phishing email
impersonating a known supplier and prepared a malicious attachment
disguised as an invoice.

DELIVERY: The phishing email containing the malicious attachment was
sent to several finance employees.

EXPLOITATION: One employee opened the attachment. The attacker exploited
an outdated software vulnerability, allowing code execution and
providing an initial foothold.

INSTALLATION: The attacker installed a backdoor and created a hidden
scheduled task to maintain access after the system restarted.

COMMAND AND CONTROL: The compromised machine quietly connected to an
attacker-controlled server, allowing the attacker to issue remote
commands and continue operating.

ACTIONS ON OBJECTIVES: The attacker explored the network, stole
credentials, moved to other systems, reached the customer database, and
copied the database to the attacker's server. The objective of stealing
customer data was achieved.

  ---------------------------------------
   3\. TECHNIQUES USED (ATT&CK thinking)
  ---------------------------------------

Stage: DELIVERY -\> Technique: Phishing email with a malicious
attachment disguised as an invoice Tactic: Initial Access

Stage: INSTALLATION -\> Technique: Hidden scheduled task used to
maintain access Tactic: Persistence

Stage: COMMAND AND CONTROL -\> Technique: Outbound connection /
beaconing to an attacker-controlled server Tactic: Command and Control

Stage: EXPLOITATION -\> Technique: Exploitation of an outdated software
vulnerability Tactic: Initial Access / Execution

  ---------------------------------------
   4\. WHERE THE CHAIN COULD HAVE BROKEN
  ---------------------------------------

Stage: DELIVERY -\> Defence: Email filtering, malicious-attachment
analysis, and phishing awareness/reporting could have prevented the
attachment from being opened.

Stage: EXPLOITATION -\> Defence: Patching the outdated software could
have prevented the vulnerability from being exploited.

Stage: INSTALLATION -\> Defence: Monitoring for unexpected scheduled
tasks and other persistence mechanisms could have exposed the attacker's
persistence.

Stage: COMMAND AND CONTROL -\> Defence: Monitoring for unusual outbound
connections and beaconing could have detected communication with the
attacker's server.

Stage: ACTIONS ON OBJECTIVES -\> Defence: Monitoring sensitive database
access and large or unusual outbound data transfers could have detected
the theft.

MOST EFFECTIVE DEFENCE:

Patching the outdated software would have been the most effective
defence in this scenario. The attacker needed the vulnerability to turn
the opened attachment into code execution and gain an initial foothold.
If the software had been patched, the exploit described in the scenario
could have failed, preventing the later stages of the attack.

  -----------------------------
   5\. LESSONS THAT GENERALISE
  -----------------------------

This analysis shows that successful attacks are usually a sequence of
connected activities rather than a single event. Organisations therefore
need multiple layers of defence.

Important defensive lessons include:

-   Reduce unnecessary public information that can support targeted
    social engineering.
-   Use email filtering and attachment analysis to detect malicious
    messages.
-   Keep software patched to reduce exploitable vulnerabilities.
-   Monitor for unexpected persistence mechanisms such as scheduled
    tasks.
-   Monitor outbound network traffic for unusual connections and
    beaconing.
-   Monitor credential use and lateral movement between systems.
-   Protect sensitive databases and monitor unusual data access and
    large outbound transfers.

Although this was a simulated scenario, analysing it felt different from
simply studying the frameworks. I had to follow the attack step by step,
identify what the attacker achieved at each stage, and then think about
where a defender could have interrupted the chain. This made the
frameworks feel more practical and closer to the way an analyst
structures an incident.

For this analysis, the Kill Chain was more useful for building the
overall attack story because it provided a clear sequence from
reconnaissance to the final objective. ATT&CK thinking was more useful
for adding detail about the specific methods used at individual stages.
Using both together gave a clearer view of the attack and the available
defensive opportunities.

  ------------------
   6\. KEY TAKEAWAY
  ------------------

The biggest insight from this analysis is that an attacker must
successfully progress through multiple stages, while a defender only
needs to break the chain at one effective point.

In this scenario, there were several opportunities to stop the attack
--- especially phishing detection, patching, persistence monitoring, C2
detection, and data-transfer monitoring. The exercise showed me how the
Kill Chain helps identify WHERE an attack is happening, while ATT&CK
thinking helps explain HOW the attacker is carrying it out.

============================================================ END OF
ANALYSIS ============================================================
