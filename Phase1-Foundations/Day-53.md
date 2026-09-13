# Day 53 — Reading Files in Linux 🐧

## 📌 Overview

Day 53 focused on **reading and searching files in Linux**, especially files that can contain system information, configuration details, and security-related events.

In security investigations, information is often stored inside files and logs. The challenge is not simply reading files, but knowing **which tool to use to find the information that matters efficiently**.

Today I learned and practiced:

- `cat`
- `less`
- `head`
- `tail`
- `tail -f`
- `grep`
- Useful `grep` options such as `-i`, `-n`, `-r`, `-v`, and `-c`
- Using these commands to investigate Linux files and logs

---

## 🎯 Learning Objectives

By the end of this task, I wanted to understand:

- How to read the contents of a Linux file
- Why `cat` is not always suitable for large files
- How to navigate large files using `less`
- How to inspect the beginning and end of files
- How to monitor logs for new entries
- How to search for specific information using `grep`
- How filtering can make security investigations more efficient

---

# 1. `cat` — Reading the Entire File

The `cat` command displays the complete contents of a file.

### Syntax

```bash
cat filename
```

### Example

```bash
cat /etc/hostname
```

### Result

The command displayed the hostname of my Linux environment:

```text
DESKTOP-A2AB4OS
```

### When to use `cat`

`cat` is useful when the file is small and I want to see its entire contents quickly.

### Limitation

For a very large file, `cat` can display thousands of lines at once and flood the terminal.

For large files, a pager such as `less` is more practical.

---

# 2. `less` — Exploring Large Files

The `less` command allows a file to be viewed one screen at a time.

### Example

```bash
less /etc/services
```

Instead of displaying the entire file immediately, `less` allows me to:

- Scroll through the file
- Move up and down
- Search for specific text
- Exit when finished

### Searching inside `less`

I used:

```text
/https
```

The search located HTTPS entries in `/etc/services`.

Relevant entries included:

```text
https 443/tcp
https 443/udp
```

This showed that the `/etc/services` file contains mappings between service names, port numbers, and protocols.

### Exit

```text
q
```

---

# 3. `head` — Viewing the Beginning of a File

The `head` command displays the beginning of a file.

```bash
head /etc/services
```

By default, `head` displays the first **10 lines**.

A specific number of lines can be requested using `-n`.

```bash
head -n 20 /etc/services
```

This displays the first 20 lines.

### Security usefulness

`head` is useful when I want a quick look at the beginning of an unfamiliar file without reading the entire file.

---

# 4. `tail` — Viewing the End of a File

The `tail` command displays the end of a file.

```bash
tail /etc/services
```

By default, it displays the last **10 lines**.

A specific number can be selected:

```bash
tail -n 20 /etc/services
```

### Why `tail` is useful for logs

Recent log entries are commonly found near the end of a log file.

I used:

```bash
tail /var/log/syslog
```

This displayed recent system activity, including events involving system services, WSL activity, kernel messages, and time synchronization.

One important lesson was that a warning or error in a log **is not automatically a security incident**. It needs to be investigated and interpreted in context.

---

# 5. `tail -f` — Following Logs

The `-f` option allows `tail` to continue monitoring a file.

```bash
tail -f /var/log/syslog
```

New lines are displayed as they are added to the file.

This can be useful when monitoring a system or service while it is actively generating events.

To stop following the file:

```text
Ctrl + C
```

---

# 6. `grep` — Searching File Contents

`grep` is used to search for specific text inside files.

### Syntax

```bash
grep "term" filename
```

For example:

```bash
grep "error" /var/log/syslog
```

This displays only the lines containing the word `error`.

Instead of manually reading an entire log, I can quickly focus on lines that contain a particular term.

---

# 7. Useful `grep` Options

## `-i` — Case-Insensitive Search

```bash
grep -i "failed" /var/log/auth.log
```

The `-i` option ignores differences in capitalization.

It can therefore match variations such as:

```text
failed
Failed
FAILED
```

In my task, this search produced no output.

This means that **no matching `failed` lines were found in that particular search**. It does not prove that failed login attempts have never occurred.

---

## `-n` — Display Line Numbers

```bash
grep -n "https" /etc/services
```

The result included:

```text
83:https 443/tcp
84:https 443/udp
```

The numbers show the lines where the matching text was found.

---

## `-c` — Count Matching Lines

```bash
grep -c "tcp" /etc/services
```

Result:

```text
220
```

This means there were **220 lines containing the matching term `tcp`**.

### Difference between normal `grep` and `grep -c`

```bash
grep "tcp" /etc/services
```

Displays the matching lines.

```bash
grep -c "tcp" /etc/services
```

Displays only the number of matching lines.

---

## `-r` — Recursive Search

```bash
grep -r "keyword" /path/to/directory
```

The `-r` option searches through files within a directory and its subdirectories.

This is useful when I know what information I am looking for but do not know which file contains it.

---

## `-v` — Show Non-Matching Lines

```bash
grep -v "error" filename
```

This displays lines that do **not** contain the specified search term.

---

# 8. Security Investigation Use Cases

These commands can be applied to common security investigation tasks.

### Check recent system activity

```bash
tail /var/log/syslog
```

### Search for failed authentication attempts

```bash
grep -i "failed" /var/log/auth.log
```

### Search for errors

```bash
grep -i "error" /var/log/syslog
```

### Find a specific service or port

```bash
grep -i "https" /etc/services
```

### Count matching entries

```bash
grep -c "tcp" /etc/services
```

The important idea is that the command should match the question I am trying to answer.

---

# 9. Choosing the Right Tool

| Situation | Command |
|---|---|
| Read a small file completely | `cat` |
| Explore a large file | `less` |
| Search inside `less` | `/word` |
| View beginning of file | `head` |
| View end of file | `tail` |
| View a specific number of lines | `head -n` / `tail -n` |
| Follow a changing log | `tail -f` |
| Search file contents | `grep` |
| Ignore capitalization | `grep -i` |
| Show line numbers | `grep -n` |
| Count matching lines | `grep -c` |
| Search directories recursively | `grep -r` |
| Show non-matching lines | `grep -v` |

---

# 10. Investigation Mindset

A useful workflow for Linux file investigation is:

```text
Identify the question
        ↓
Choose the appropriate tool
        ↓
Filter unnecessary information
        ↓
Examine relevant results
        ↓
Interpret the results
```

For example:

**Question:** What happened recently?

```bash
tail /var/log/syslog
```

**Question:** Are there lines containing an error?

```bash
grep -i "error" /var/log/syslog
```

**Question:** How many lines contain `tcp`?

```bash
grep -c "tcp" /etc/services
```

**Question:** Where is HTTPS listed?

```bash
grep -n "https" /etc/services
```

The commands help surface information, but the investigator still needs to determine **what the information means**.

---

# 11. Key Security Lessons

### 🔹 Don't read everything manually

Large logs may contain thousands of lines. Searching and filtering can dramatically reduce the amount of information that needs to be examined.

### 🔹 Choose tools based on the question

Different commands solve different problems.

- Need the whole small file → `cat`
- Need to explore a large file → `less`
- Need recent activity → `tail`
- Need the beginning → `head`
- Need specific content → `grep`

### 🔹 Errors are not automatically attacks

A log entry containing `error` or `warning` does not automatically indicate malicious activity.

It is an **indicator that may require investigation**, not proof of compromise.

### 🔹 No result is still a result

If `grep` produces no output, it means that no matching lines were found for that search.

It should not automatically be interpreted as proof that the event never happened.

---

# 🧪 Practical Task Summary

During today's hands-on task, I:

1. Used `cat` to read `/etc/hostname`.
2. Used `less` to explore `/etc/services`.
3. Searched inside `less` using `/https`.
4. Found HTTPS entries associated with port `443`.
5. Used `head` to inspect the beginning of `/etc/services`.
6. Used `tail` to inspect the end of `/etc/services`.
7. Used `tail` on `/var/log/syslog` to examine recent system activity.
8. Used `grep` to search for errors.
9. Used `grep -i` to search for failed authentication entries.
10. Used `grep -n` to identify line numbers.
11. Used `grep -c` and found **220 matching `tcp` lines**.
12. Practiced thinking about which command best answers a particular investigation question.

---

# 💡 Final Takeaway

Day 53 showed me that reading files in Linux is not simply about opening a file and looking at everything inside it.

It is about **finding the relevant information efficiently**.

Commands such as `less`, `head`, `tail`, and `grep` allow a security analyst to reduce noise and focus on useful evidence.

> **A security investigator doesn't need to read everything. They need to know how to find the information that matters.**

---

## 📚 Commands Practiced

```bash
cat /etc/hostname

less /etc/services

head /etc/services

head -n 20 /etc/services

tail /etc/services

tail -n 20 /etc/services

tail /var/log/syslog

grep "error" /var/log/syslog

grep -i "https" /etc/services

grep -n "https" /etc/services

grep -c "tcp" /etc/services

grep -i "failed" /var/log/auth.log
```

---

**Day 53/90 — Linux Phase 🐧**

**Focus:** Reading, searching, filtering, and investigating files in Linux.