# Day 62 — Cron, Scheduling, Automation & Persistence ⏰🐧

## Overview

Today I learned about **cron**, Linux's built-in scheduling system for automatically running commands or scripts at specific times.

Cron is commonly used for backups, log processing, maintenance, monitoring, and cleanup. However, scheduled tasks can also be abused for **persistence**.

---

## What is Cron?

**Cron** is a Linux scheduling system that runs commands or scripts automatically according to a schedule.

A scheduled task is called a **cron job**, and a user's scheduled jobs are stored in their **crontab**.

### Common legitimate uses

- Backups
- Log processing and rotation
- System maintenance
- Security checks
- Monitoring
- Cleanup tasks
- Automated scripts

---

## Cron Job Structure

A cron job contains five scheduling fields followed by the command:

```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week
│ │ │ └──── Month
│ │ └────── Day of month
│ └──────── Hour
└────────── Minute
```

| Field | Meaning |
|---|---|
| Minute | 0–59 |
| Hour | 0–23 |
| Day of month | 1–31 |
| Month | 1–12 |
| Day of week | 0–7 |

The `*` symbol means every possible value for that field.

For example:

```text
* * * * * command
```

runs the command every minute.

---

## User Crontab and System Cron Locations

### User crontab

View scheduled jobs:

```bash
crontab -l
```

Edit scheduled jobs:

```bash
crontab -e
```

### System cron locations

Important system locations include:

```text
/etc/cron.d/
/etc/cron.daily/
/etc/cron.hourly/
/etc/cron.weekly/
/etc/cron.monthly/
```

These are important during security investigations because suspicious scheduled tasks may exist outside a user's personal crontab.

---

# Cron and Persistence

**Persistence** means maintaining access or the ability to continue malicious activity after the original access method or process is no longer active.

Cron can be abused for persistence because a scheduled job remains configured and can execute a command or script again at its scheduled time.

For example:

```text
Malicious process stopped
        ↓
Cron job still exists
        ↓
Scheduled time arrives
        ↓
Malicious command runs again
```

Therefore, stopping a process alone may not completely remove persistence.

A scheduled task is not automatically malicious. Cron is also heavily used for legitimate system administration, so investigators need to examine its context.

---

# Privileged Cron Jobs and Security Risk

A particularly dangerous situation occurs when a cron job runs with **root privileges** while executing a script that an ordinary user can modify.

```text
Root cron job
      ↓
Runs a script with root privileges
      ↓
Ordinary user can modify the script
      ↓
Modified commands execute as root
```

This can create a **privilege-escalation risk**.

The key principle is:

> A privileged process should not execute files that untrusted users can modify.

---

# Hands-On Task

## Step 1 — Check Existing User Cron Jobs

I checked whether my Ubuntu user already had scheduled jobs:

```bash
crontab -l
```

Output:

```text
no crontab for shikha
```

This showed that my user did not have an existing personal crontab.

---

## Step 2 — Inspect System Cron Directories

I checked:

```bash
ls /etc/cron.d
```

Output included:

```text
e2scrub_all
```

I also checked:

```bash
ls /etc/cron.daily
```

Output included:

```text
apport
apt-compat
dpkg
logrotate
man-db
```

This demonstrated that cron is a normal part of Linux system maintenance.

---

## Step 3 — Create a Test Cron Job

I opened the user's crontab:

```bash
crontab -e
```

I added:

```text
* * * * * date >> $HOME/crontest.txt
```

This scheduled the `date` command to run every minute and append its output to:

```text
$HOME/crontest.txt
```

When saved, the system reported:

```text
no crontab for shikha - using an empty one
crontab: installing new crontab
```

---

## Step 4 — Verify the Cron Job

After allowing the task to run, I checked:

```bash
cat $HOME/crontest.txt
```

The file contained:

```text
Wed Sep 23 04:57:01 UTC 2026
Wed Sep 23 04:58:01 UTC 2026
Wed Sep 23 04:59:02 UTC 2026
Wed Sep 23 05:00:01 UTC 2026
```

The repeated timestamps showed that the cron job was executing approximately once every minute.

---

## Step 5 — Clean Up

I removed the test cron entry with:

```bash
crontab -e
```

Then I verified the crontab:

```bash
crontab -l
```

The crontab was empty.

I removed the generated file:

```bash
rm $HOME/crontest.txt
```

Finally:

```bash
ls $HOME/crontest.txt
```

The system reported that the file did not exist, confirming that the test environment was cleaned up.

---

# Investigation Perspective

When investigating suspicious activity, useful questions include:

- What command is scheduled?
- Which user owns the scheduled task?
- When does it run?
- What file or script does it execute?
- Where is that file located?
- Who can modify the file?
- Is the scheduled task expected?
- Does it download, execute, or recreate suspicious files?
- Does it connect to an unusual destination?
- Is it running with elevated privileges?

The goal is to understand the **context** rather than automatically treating every cron job as malicious.

---

# Connections to Previous Linux Topics

### File Permissions

A root cron job executing a user-writable script demonstrates why Linux permissions matter.

### Users and Groups

The account executing a scheduled task determines the privileges available to the command.

### Processes

Cron starts commands as processes according to their schedules.

### Scripting

Cron can automate scripts, making scripting useful for administration and security operations.

### Security Investigation

Scheduled tasks can provide clues about how suspicious activity starts or persists.

---

# Safe Cron Practices

- Review scheduled jobs regularly.
- Keep privileged scripts protected with appropriate permissions.
- Avoid unnecessary commands running as root.
- Ensure privileged scheduled scripts cannot be modified by untrusted users.
- Remove unused scheduled tasks.
- Monitor unexpected changes to cron configuration.
- Investigate unusual scheduled commands during incident response.

---

# Key Takeaways

- **Cron** is Linux's scheduling system.
- A **cron job** is a scheduled task.
- **Crontab** stores a user's scheduled jobs.
- Cron is widely used for legitimate automation and maintenance.
- Scheduled tasks can also be abused for **persistence**.
- Stopping a malicious process does not necessarily remove a malicious cron job.
- System locations such as `/etc/cron.d` and `/etc/cron.daily` matter during investigations.
- A root cron job executing a script writable by an ordinary user can create a privilege-escalation risk.
- Cron jobs should be evaluated in context rather than automatically treated as malicious.
- Investigators should ask **what runs, who runs it, what it executes, and when it runs**.

---

## Day 62 Summary

Today's task showed me that automation is not only about convenience.

The same scheduling mechanism that helps Linux perform routine maintenance can also become a persistence mechanism when abused.

From a cybersecurity perspective, understanding **what is scheduled, who controls it, what privileges it has, and what it executes** can reveal important clues during an investigation.

**Day 62 complete. ⏰🐧🔐**
