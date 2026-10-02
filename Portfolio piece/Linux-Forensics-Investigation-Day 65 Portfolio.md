============================================================
 LINUX FORENSICS INVESTIGATION
============================================================

Investigator:    Shikha
Date:            26 September 2026
System examined: WSL2 Linux practice environment
Scenario:        Suspected compromise (staged practice scenario)
Method:          Live + historical examination; suspicious files
                 examined without execution


------------------------------------------------------------
 1. SUMMARY
------------------------------------------------------------

- Controlled Linux forensics exercise using harmless,
  investigator-created evidence.
- Reviewed processes, network connections, authentication logs,
  accounts, scheduled tasks, and recently modified files.
- No obvious evidence of a real compromise was identified in
  the evidence examined.
- The staged /tmp/update.sh file was plain ASCII text,
  non-executable, and contained harmless placeholder content;
  it was examined but never executed.
- Confidence: MEDIUM, because this was a staged scenario and
  the investigation covered selected evidence rather than a
  full forensic acquisition.


------------------------------------------------------------
 2. INVESTIGATOR'S CHECKLIST FINDINGS
------------------------------------------------------------

PROCESSES (what's running that shouldn't be):
  - Reviewed running processes with `ps aux`.
  - Observed normal-looking Linux/WSL system processes, service
    accounts, and user shell processes.
  - No obviously abnormal CPU or memory usage was identified.
  - Some command names were truncated in the terminal output,
    so unfamiliar processes would require further investigation
    in a real incident.
  - Look for: unusual names or paths, high resource usage,
    unexpected privileges, and suspicious parent/child processes.

NETWORK CONNECTIONS (what it's talking to):
  - Reviewed network state with `ss -tuln` and `ss -tunap`.
  - Port 53 listeners were observed for DNS-related activity.
  - Port 323 was observed on local addresses for time
    synchronisation activity.
  - No obviously suspicious established external connection
    was identified in the captured output.
  - Process mapping was not available in the captured socket
    output, so no process was attributed to a socket without
    evidence.
  - Look for: unexpected listeners, unknown remote destinations,
    unusual outbound connections, and process-to-network links.

LOGS (the history / timeline):
  - Reviewed the available tail of `/var/log/auth.log`.
  - Observed normal user session activity for the investigator
    account.
  - Observed a root CRON session opening and closing.
  - Observed a sudo session used during the investigation.
  - No failed-login-then-success pattern was visible in the
    captured log section.
  - Look for: failed logins, unusual successful logins, account
    creation, privilege changes, and suspicious sudo activity.

ACCOUNTS (who exists / who can sudo):
  - Reviewed `/etc/passwd` for system and user accounts.
  - The expected investigator account was present with a normal
    home directory and Bash shell.
  - Reviewed sudo membership with `getent group sudo`.
  - No unexplained rogue account was identified.
  - Look for: unexpected accounts, unusual UIDs, interactive
    shells on service accounts, and unexpected sudo membership.

SCHEDULED TASKS (persistence):
  - Reviewed the user's cron configuration with `crontab -l`.
  - No user-level cron job was present.
  - Reviewed `/etc/cron.d`; `e2scrub_all` was present.
  - The system cron entry was not treated as malicious based
    only on its filename.
  - `evidence_note.txt` was only a training marker and was not
    an actual cron persistence mechanism.
  - Look for: unexplained commands, unusual script locations,
    writable scripts run with elevated privileges, and tasks
    that could relaunch unwanted activity.

FILES (suspicious files):
  - Investigated `/tmp/update.sh` without executing it.
  - File type: ASCII text.
  - Size: 38 bytes.
  - Permissions: `-rw-r--r--`.
  - Owner/group: investigator account.
  - Modified: 26 September 2026 at 11:16 UTC.
  - Contents were harmless placeholder text created for the
    exercise.
  - Recently modified file searches also identified the two
    harmless staged marker files and normal system/application
    files.
  - Recent modification was treated as an investigation lead,
    not automatic proof of malicious activity.


------------------------------------------------------------
 3. TIMELINE OF EVENTS
------------------------------------------------------------

  26 Sep, 11:14:45 UTC - Investigator's Linux user session
                           opened.

  26 Sep, 11:16 UTC    - Harmless staged `/tmp/update.sh` was
                           created/modified for the investigation.

  26 Sep, 11:17:01 UTC - A root CRON session opened and closed.

  Investigation phase   - Running processes were reviewed for
                           unusual or unexpected activity.

  Investigation phase   - Listening sockets and current network
                           state were examined.

  Investigation phase   - Authentication logs were reviewed for
                           login, sudo, and CRON activity.

  Investigation phase   - Accounts and sudo membership were
                           reviewed.

  Investigation phase   - User and system cron configuration was
                           reviewed for persistence.

  Investigation phase   - Recently modified files were searched,
                           and `/tmp/update.sh` was examined safely.

  26 Sep, 12:08:15 UTC - Investigator used sudo to review the
                           authentication log.

  After investigation  - Staged evidence was removed as part of
                           cleanup.

  Note: This timeline represents a controlled training scenario.
  The staged files were created by the investigator and do not
  represent a real intrusion.


------------------------------------------------------------
 4. VERDICT AND CONFIDENCE
------------------------------------------------------------

Verdict:     NOT COMPROMISED (within the evidence examined)
Confidence:  MEDIUM

Evidence-based reasoning:
  - No obviously malicious process was identified.
  - No obviously suspicious established external connection
    was identified.
  - The examined authentication-log section showed no obvious
    failed-login-then-success pattern.
  - No unexplained account or suspicious user cron job was found.
  - `/tmp/update.sh` was intentionally staged, contained harmless
    placeholder content, and was never executed.
  - The investigation was limited to selected live state, logs,
    configuration, and recent-file evidence.
  - A real incident would require broader historical analysis
    and potentially disk or memory acquisition.
  - The verdict does not prove that the system has never been
    compromised; it reflects only the evidence examined.


------------------------------------------------------------
 5. HOW THE ATTACKER GOT IN AND STAYED
------------------------------------------------------------

Entry:
  - No real attacker entry was established because this was a
    staged practice scenario.
  - In a real incident, correlate authentication logs, network
    activity, exposed services, vulnerabilities, and account
    activity to identify the entry point.

Actions:
  - No real attacker actions were observed.
  - The harmless staged `/tmp/update.sh` represented a
    suspicious-file finding for investigation.
  - The file was examined without execution.

Persistence:
  - No actual persistence mechanism was identified.
  - The user's cron was empty.
  - `/etc/cron.d` contained `e2scrub_all`, which was not treated
    as malicious without further evidence.
  - `evidence_note.txt` was only a training marker, not an
    actual cron persistence mechanism.


------------------------------------------------------------
 6. RECOMMENDATIONS
------------------------------------------------------------

  [x] Remove the staged evidence after completing the
      investigation.
  [ ] Preserve relevant evidence before making changes in a
      real incident.
  [ ] Review authentication, system, kernel, and application
      logs over a wider historical period.
  [ ] Investigate unexpected processes and correlate them with
      executable paths, users, timestamps, and network
      connections.
  [ ] Find and review all persistence mechanisms, including
      cron, systemd services, SSH keys, and startup configuration.
  [ ] Remove rogue accounts and reset compromised credentials
      if evidence supports compromise.
  [ ] Apply Linux hardening: updates, least privilege, reduced
      unnecessary services, secure remote access, and monitoring.
  [ ] Escalate according to the incident-response process if
      stronger evidence of compromise is discovered.


------------------------------------------------------------
 7. SCOPE AND LIMITATIONS
------------------------------------------------------------

  - Controlled learning exercise using harmless,
    investigator-created evidence.
  - No real malware was introduced or executed.
  - The suspicious file was examined safely without execution.
  - The investigation covered processes, network connections,
    logs, accounts, scheduled tasks, and files.
  - The exercise demonstrated how individual findings can be
    connected into a timeline and evaluated as evidence.
  - A real investigation would add broader historical log
    analysis, process-to-network correlation, persistence checks
    beyond cron, file integrity analysis, and potentially memory
    or disk imaging.
  - Because this was staged, the findings demonstrate
    investigative method rather than evidence of a real attack.


============================================================
 END OF INVESTIGATION
============================================================
