# Day 65 --- Linux Forensics Investigation

## Task

The task was to investigate a Linux system as if it might have been
compromised and reconstruct what happened using evidence.

This was a controlled practice scenario using harmless,
investigator-created evidence. No real malware was introduced or
executed.

### Investigation Questions

-   Is the system compromised?
-   What did the attacker do?
-   How did they get in?
-   What did they touch?
-   Are they maintaining access?
-   What evidence supports the conclusion?

### Investigation Areas

#### 1. Processes

-   Reviewed running processes with `ps aux`.
-   Looked for unfamiliar processes, suspicious names or locations,
    unusual resource usage, unexpected privileges, and suspicious
    parent/child relationships.
-   No obviously abnormal process was identified in the captured output.

#### 2. Network Connections

-   Reviewed network state with `ss -tuln` and `ss -tunap`.
-   Observed DNS-related listeners on port 53.
-   Observed local time-synchronisation activity on port 323.
-   No obviously suspicious established external connection was
    identified in the captured output.
-   Network findings were treated as evidence requiring context rather
    than automatic proof of compromise.

#### 3. Logs

-   Reviewed `/var/log/auth.log`.
-   Examined user sessions, sudo activity, CRON activity, and
    authentication events.
-   The captured log section showed normal user session activity, a root
    CRON session, and sudo activity used during the investigation.
-   No obvious failed-login-then-success pattern was visible in the
    captured section.

#### 4. Accounts

-   Reviewed `/etc/passwd`.
-   Checked sudo membership with `getent group sudo`.
-   Looked for unexpected accounts, unusual user IDs, interactive shells
    on service accounts, and unexpected sudo privileges.
-   No unexplained rogue account was identified.

#### 5. Scheduled Tasks and Persistence

-   Checked the user cron configuration with `crontab -l`.
-   Reviewed `/etc/cron.d`.
-   No user-level cron job was present.
-   `e2scrub_all` was present as a system cron entry and was not treated
    as malicious based only on its filename.
-   The investigation also considered other persistence mechanisms that
    would need to be checked during a real incident.

#### 6. Suspicious and Recently Modified Files

-   Created harmless staged evidence for the exercise.
-   Investigated `/tmp/update.sh` without executing it.
-   File type: ASCII text.
-   Permissions: `-rw-r--r--`.
-   Owner/group: investigator account.
-   The file contained harmless placeholder content.
-   Recent-file searches were performed in `/tmp` and the home
    directory.
-   Recently modified files were treated as investigation leads rather
    than automatically malicious evidence.
-   Suspicious files should be examined safely and should not be
    executed during an investigation.

#### 7. Timeline Reconstruction

-   Individual findings were considered together rather than in
    isolation.
-   Timestamps were used to establish the order of events.
-   The investigation followed the general sequence: processes → network
    activity → logs → accounts → persistence → files → timeline →
    verdict.

## Task Result

-   The evidence examined did not show an obvious real compromise.
-   The suspicious file was intentionally staged for the exercise.
-   No real attacker entry, actions, or persistence mechanism were
    established.
-   The investigation demonstrated how evidence from different parts of
    a Linux system can be connected to reconstruct a possible incident.
-   Confidence was kept at a realistic level because this was a
    controlled practice scenario and not a complete forensic
    acquisition.

## Key Takeaways

-   Linux forensics is about evidence and reasoning, not simply running
    commands.
-   An unfamiliar process is not automatically malicious.
-   A listening port is not automatically evidence of an attacker.
-   A recently modified file is not automatically malicious.
-   Authentication logs can help establish a timeline of activity.
-   Accounts and sudo membership can reveal unexpected access or
    privilege.
-   Cron jobs and other scheduled tasks can be used for persistence.
-   Suspicious files should be investigated without executing them.
-   Individual findings become more useful when correlated with
    timestamps and other evidence.
-   A professional investigation should clearly separate what was
    observed, what the evidence suggests, and what remains uncertain.
-   A defensible conclusion should include both the evidence supporting
    it and the limitations of the investigation.
-   Core investigative mindset: **Question → Evidence → Interpretation →
    Next Question**

## Safety Note

-   The investigation used harmless, self-created evidence.
-   No real malware was introduced.
-   The staged suspicious file was examined but never executed.
-   Staged evidence was intended only for practising the forensic
    investigation workflow.
