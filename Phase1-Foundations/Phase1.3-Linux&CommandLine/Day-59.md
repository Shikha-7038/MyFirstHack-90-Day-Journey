# Day 59 — Linux Logs & Security Investigation

## Topic

**Linux Logs: Reading the System's Memory**

Today focused on understanding Linux logs, where they are stored, how to read them efficiently, and how investigators use them to reconstruct what happened on a system.

> **Processes show what is happening now, network connections show what the system is communicating with, and logs show what has happened over time.**

---

## 1. What Are Linux Logs?

Logs are records of events that happen on a Linux system.

They can record:

- Authentication events
- Failed and successful logins
- `sudo` activity
- Services starting and stopping
- System activity
- Application activity
- Security-related events
- Other important system changes

Logs are especially useful during security investigations because they preserve a **history of system activity**.

A running process gives an investigator a snapshot of the present, while logs can help reconstruct what happened before the investigation began.

---

## 2. What Lives in `/var/log`

Most traditional Linux log files are stored under:

```text
/var/log
```

The exact files vary between Linux distributions, but several important categories are common.

### Authentication Log

Ubuntu/Debian commonly use:

```text
/var/log/auth.log
```

Some other Linux systems use:

```text
/var/log/secure
```

Authentication logs can contain:

- Successful logins
- Failed login attempts
- Logouts
- `sudo` activity
- Authentication and access-related events

This is often one of the first logs an investigator checks during a security investigation.

### System Log

Ubuntu/Debian commonly use:

```text
/var/log/syslog
```

Other Linux systems may use:

```text
/var/log/messages
```

System logs contain broader system activity, including:

- Services starting and stopping
- System events
- Activity from system components
- Hardware-related activity
- Other general messages

System logs are usually noisier than authentication logs.

### Application and Service Logs

Applications and services may maintain their own logs.

For example:

- Web servers → request and error activity
- Databases → database activity
- Package management → software installation/update activity
- Other services → service-specific events

When investigating a particular service, its own logs can provide important evidence.

### Linux Journal

Modern Linux systems using `systemd` may also maintain a structured journal.

It can be queried with:

```bash
journalctl
```

`journalctl` provides built-in filtering capabilities, such as:

- Time
- Service
- Priority
- Boot

Traditional log files and the journal may coexist.

---

## 3. Reading Logs With Existing Tools

The file-reading tools learned during Days 53–55 are directly useful for log investigation.

### `tail`

Shows recent entries:

```bash
tail /var/log/syslog
```

Logs normally grow toward the bottom, so `tail` provides a quick view of recent activity.

**Investigation question:**  
> What just happened?

### `tail -f`

Follows a log as new entries arrive:

```bash
tail -f /var/log/auth.log
```

This can be useful when monitoring authentication activity in real time.

Press `Ctrl+C` to stop following the file.

### `less`

Useful for reading large logs:

```bash
less /var/log/syslog
```

It allows you to:

- Scroll through the file
- Search within the file
- Move through large amounts of information
- Read the file without dumping everything into the terminal

Press `q` to exit.

### `grep`

Used to extract relevant lines:

```bash
grep "Failed" /var/log/auth.log
```

It can search for:

- Failed authentication
- Usernames
- Dates
- Times
- Error messages
- Specific services
- Other keywords

Case-insensitive searches can be performed with:

```bash
grep -i "failed" /var/log/auth.log
```

The main idea is:

> **Don't read everything. Ask the log a specific question.**

---

## 4. Pipes and Log Analysis

The pipelines learned on Day 55 become especially useful when working with logs.

For example:

```bash
grep "failed" auth.log | wc -l
```

This combines:

```text
Search → Count
```

More complex analysis can use:

```text
grep → sort → uniq → wc
```

This can help investigators answer:

- How many failed attempts occurred?
- Which source appeared repeatedly?
- Which account was targeted?
- How often did something occur?

The goal is to transform large amounts of raw log data into a smaller amount of useful evidence.

---

## 5. Finding the Story in Logs

Logs are not just collections of messages. They can help reconstruct an incident.

A possible authentication-related sequence might look like:

```text
Failed login
      ↓
Failed login
      ↓
Failed login
      ↓
Successful login
      ↓
Account creation
      ↓
Privilege escalation
      ↓
Other system activity
```

Individually, each event is only one piece of evidence.

When events are arranged according to their timestamps, they can form a possible incident timeline.

> **A pattern is an investigation lead, not automatically proof of compromise.**

---

## 6. Why Timestamps Matter

Log entries are associated with timestamps.

Timestamps allow investigators to determine:

- When an event occurred
- Which event happened first
- What happened immediately before an incident
- What happened afterward
- Whether different events occurred close together

This makes logs the **temporal backbone** of an investigation.

For example:

```text
10:01 → Failed authentication
10:02 → Failed authentication
10:03 → Successful authentication
10:05 → Account change
10:07 → Privileged activity
```

The timestamps turn individual events into a sequence.

---

## 7. Investigator Mindset

A good investigator starts with a question rather than randomly reading everything.

A useful workflow is:

```text
Start with a question
        ↓
Identify the relevant log
        ↓
Extract relevant events
        ↓
Compare timestamps
        ↓
Correlate with other evidence
        ↓
Interpret the evidence
```

Examples:

### Question: When did an account last log in?

Search the authentication log for that account and examine its timestamps.

### Question: Were there failed attempts before a successful login?

Search for authentication failures and compare them with the successful event.

### Question: What happened around a suspected compromise?

Focus on the relevant time window and examine activity before and after it.

### Question: Was `sudo` used?

Look for privilege-related activity in the authentication log.

---

## 8. The Investigative Triad

Day 59 completes the three-view investigation model.

| Day | Evidence | Main Question |
|---|---|---|
| Day 57 | Processes | What is running right now? |
| Day 58 | Network | What is it communicating with? |
| Day 59 | Logs | What happened over time? |

These views complement each other:

```text
PROCESS
What's running?
      ↓
NETWORK
What is it communicating with?
      ↓
LOGS
When did it happen?
What happened before and after?
      ↓
TIMELINE
      ↓
INCIDENT UNDERSTANDING
```

A suspicious process may lead to a network connection. The network connection may lead to a particular time period. Logs can then help reconstruct what happened around that time.

---

# 9. Hands-On Investigation

## Step 1 — Identify the Logs

The `/var/log` directory was examined to identify important logs.

The system contained:

```text
auth.log
syslog
journal/
```

Important categories:

- `auth.log` → authentication and access events
- `syslog` → general system and service activity
- `journal/` → systemd journal data

## Step 2 — Examine Recent System Activity

Recent system activity was viewed using:

```bash
tail /var/log/syslog
```

The output contained timestamped activity from components such as:

- Snap
- systemd
- WSL-related services
- Linux kernel

This demonstrated that `tail` provides a quick view of recent system activity.

## Step 3 — Examine Authentication Activity

The authentication log was read using:

```bash
sudo tail /var/log/auth.log
```

A `sudo` activity entry was identified.

The log recorded information including:

- The account using `sudo`
- The target user
- The command executed
- The terminal
- The working directory
- The time of the activity

This demonstrated the Day 52 concept that **privilege elevation can leave an audit trail**.

## Step 4 — Search for Failed Logins

The authentication log was searched using:

```bash
sudo grep "Failed" /var/log/auth.log
```

The search returned a matching entry, but it was not a failed login.

It was the authentication log recording the `grep` command itself.

This was an important investigation lesson:

> **A matching search result is not automatically the evidence you are looking for. The investigator must interpret what generated the entry.**

No actual failed-login event was identified by this search.

This should not be interpreted as proof that no failed login ever occurred; it only describes the result of the particular search performed.

## Step 5 — Query the Journal

The system journal was available and queried using:

```bash
journalctl -n 20
```

The journal displayed recent events from different system components, including:

- System services
- WSL-related activity
- Time synchronization
- `sudo` activity

This demonstrated that `journalctl` can provide a recent, filtered view of system records.

---

# 10. Connection With Previous Days

### Day 48
Learned about `/var/log` and the idea that Linux stores important system information in files and file-like interfaces.

### Day 52
Learned about users, groups, root, `sudo`, and privilege escalation. Day 59 showed how `sudo` activity can appear in authentication logs.

### Days 53–55
Learned `tail`, `less`, `grep`, pipes, `wc`, `sort`, and `uniq`. These now form a practical log-analysis toolkit.

### Day 38
Learned why logs matter during security investigations.

### Day 39
Learned about forensic timelines and reconstructing events.

### Day 57
Learned how to investigate running processes.

### Day 58
Learned how to investigate network connections.

### Day 59
Combined these ideas with historical system records.

---

# 11. Present, Connections, and History

A useful way to remember the last three days:

```text
DAY 57
Processes
"What is happening now?"

        +

DAY 58
Network
"What is it communicating with?"

        +

DAY 59
Logs
"What happened over time?"

        ↓

Complete Investigative Picture
```

Processes and network connections provide a view of the current state.

Logs provide the historical context needed to understand how the system reached that state.

---

# 12. Key Takeaways

- Linux logs preserve a record of system activity.
- `/var/log` contains many important traditional log files.
- `auth.log` is especially important for authentication and access-related investigation.
- `syslog` provides broader system and service activity.
- Applications and services can maintain their own logs.
- `journalctl` provides access to the systemd journal.
- `tail` is useful for recent activity.
- `tail -f` can monitor new entries as they arrive.
- `less` is useful for navigating large logs.
- `grep` extracts relevant events from large amounts of data.
- Pipes allow multiple analysis tools to work together.
- Timestamps allow investigators to establish the sequence of events.
- A suspicious pattern is an investigation lead, not automatically proof of compromise.
- Logs can help reconstruct an incident timeline.
- The investigative triad is **Processes + Network + Logs**.
- Good investigation starts with a question and uses the appropriate evidence source to answer it.

## Final Takeaway

> **A process and a network connection show a moment. Logs provide the history that explains how the system got there.**

Day 59 completes the Linux investigative triad and provides the foundation for correlating **processes, network activity, and logs** during incident response and digital forensics.
