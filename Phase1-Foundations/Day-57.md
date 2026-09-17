# 🐧 Day 57 — Linux Processes

## 1. What Is a Process?

A **process** is a program that is currently running.

A program stored on disk is only potential activity. Once it starts running, the operating system creates a process for it.

### File vs Process

| File | Process |
|---|---|
| What could happen | What is happening now |
| Static evidence | Live evidence |
| Exists on disk | Represents running activity |
| Investigated without executing | Investigated while active |

In cybersecurity:

> **File investigation asks: “What could this do?”**  
> **Process investigation asks: “What is happening right now?”**

---

## 2. Why Processes Matter in Cybersecurity

A compromised system may contain malicious files, but those files may not currently be running.

A malicious process, however, represents **active activity**.

A suspicious process may:

- consume CPU or memory
- access files
- run with elevated privileges
- communicate over the network
- create or modify system information
- perform malicious actions in memory

Some malware can also operate primarily in memory or leave little useful evidence on disk. Therefore, examining running processes can reveal activity that file inspection alone might miss.

### Important principle

**Processes are also evidence.**

Live process information can disappear when a system is shut down, which is why live-system investigation can be important during incident response.

---

# 3. Important Process Properties

When investigating a process, several properties are useful.

### PID — Process ID

Every running process has a **PID**, which is a unique number used to identify that process.

Example:

```text
PID 1 → systemd
```

The PID can be used when investigating or stopping a specific process.

---

### Owner

The owner tells you **which user account the process is running as**.

Examples:

```text
root
shikha
```

A process running as `root` has significantly greater privileges than one running as an ordinary user.

Therefore:

> An unfamiliar process running as root deserves closer investigation.

However, **root ownership alone does not mean the process is malicious**. Many legitimate Linux system services run as root.

---

### CPU and Memory

Processes consume system resources.

Important indicators include:

- `%CPU`
- `%MEM`

Unusually high resource consumption can be a clue.

For example, cryptocurrency-mining malware may consume substantial CPU resources.

But:

> **High CPU or memory usage alone does not prove malware.**

The investigator needs additional evidence.

---

### Parent Process

A process can be started by another process.

The process that starts another process is its **parent process**.

This creates a process relationship or family tree.

Understanding the parent can help answer:

> **“How did this process start?”**

This can be especially useful when investigating suspicious activity.

---

# 4. The `/proc` Filesystem

Linux follows the principle that much system information can be accessed through a **file-like interface**.

Running processes are represented under:

```text
/proc
```

Each process normally has a numbered directory corresponding to its PID.

For example:

```text
/proc/1
/proc/457
/proc/929
```

Here:

```text
/proc/1
```

contains information about the process with PID `1`.

A process directory can contain information such as:

- command information
- process status
- memory information
- open file descriptors
- process relationships
- namespaces
- network-related information

You do not need to memorize every `/proc` entry.

The important concept is:

> **A running process can be inspected through `/proc/<PID>`.**

---

# 5. Viewing Running Processes with `ps`

The `ps` command provides a **snapshot** of processes.

A commonly used command is:

```bash
ps aux
```

It displays information such as:

- user/owner
- PID
- CPU usage
- memory usage
- process state
- command

Each line represents a process.

### Think of `ps` as:

📸 **A photograph of the system**

It gives you a snapshot at a particular moment.

---

# 6. Monitoring Processes with `top`

The `top` command provides a **live, continuously updating view** of processes.

```bash
top
```

It allows you to observe:

- CPU usage
- memory usage
- running processes
- process IDs
- process owners
- changing resource consumption

The display updates while the system is running.

Press:

```text
q
```

to exit `top`.

### Think of `top` as:

🎥 **A live video feed of processes**

---

## `ps` vs `top`

| `ps aux` | `top` |
|---|---|
| Snapshot | Live view |
| Shows processes at one moment | Continuously updates |
| Good for methodical examination | Good for watching activity |
| Photograph 📸 | Video 🎥 |

A useful workflow is:

**`top` → spot something interesting → `ps aux` → examine it**

---

# 7. `htop`

`htop` is a more user-friendly alternative to `top`.

It provides a more visual interface for monitoring processes.

If it is already installed:

```bash
htop
```

It is useful for easier process monitoring, but it is **not essential** to understand today's lesson.

---

# 8. Identifying Suspicious Processes

A security investigator doesn't automatically assume that an unfamiliar process is malicious.

Instead, they ask:

> **“Does this process make sense on this system?”**

Potential warning signs include:

### 1. Unusually high CPU usage

A process consuming much more CPU than expected may deserve investigation.

### 2. Unusually high memory usage

Unexpectedly high memory consumption can also be a clue.

### 3. Unrecognised process

A process that is unfamiliar or unexpected should be investigated.

### 4. Running as root

An unexpected process running with root privileges deserves particular attention because of its greater access.

### 5. Unusual location

A process running from an unusual location, such as `/tmp`, can be suspicious.

### 6. Unexpected network activity

A process making unexplained network connections may require further investigation.

### Important:

> **None of these signs proves that a process is malicious by itself.**

They are **investigation clues**.

---

# 9. Process Investigation Workflow

A basic process investigation can follow this pattern:

```text
List processes
     ↓
Look for unusual behaviour
     ↓
Identify the process
     ↓
Check its PID and owner
     ↓
Investigate its resources
     ↓
Inspect /proc
     ↓
Look at network activity
     ↓
Check logs
     ↓
Connect the evidence
```

The investigator moves from observation to evidence rather than immediately assuming something is malicious.

---

# 10. Starting and Stopping a Process Safely

For practice, a harmless process can be created using:

```bash
sleep 300 &
```

The `&` runs the process in the background and returns the terminal prompt.

The system provides a PID for the process.

The process can then be identified and stopped using its PID:

```bash
kill <PID>
```

### Important distinction

`kill` does not necessarily mean “destroy immediately.”

It sends a signal to the process. The normal `kill <PID>` sends a termination request.

### Safety rule

Only stop processes that you have deliberately started for practice.

Do **not** randomly kill unfamiliar system processes because doing so can disrupt the system or your session.

---

# 11. Processes, Network Connections, and Logs

A process rarely acts completely alone.

A suspicious process may:

- make network connections
- communicate with a remote system
- generate events
- modify files
- leave log entries

This creates three connected views of an investigation:

```text
Process
   ↓
What is happening now?

Network
   ↓
What is it communicating with?

Logs
   ↓
What happened over time?
```

These are different pieces of evidence about potentially related activity.

---

# 12. Connection to Day 56

Day 56 investigated a suspicious file.

The main question was:

> **“What could this file do?”**

Day 57 moves to running activity:

> **“What is actually happening right now?”**

So the investigation progresses from:

```text
File
  ↓
Potential activity
  ↓
Process
  ↓
Active activity
  ↓
Network connections
  ↓
Logs
  ↓
Full investigation
```

This progression will become important for the later forensics work.

---

# 13. Investigator Mindset

When examining a suspicious process, ask:

### Who?

Who owns the process?

### What?

What program or command is running?

### How?

How did the process start? What is its parent process?

### Where?

Where is the program located?

### Why?

Why is this process running on the system?

### What else?

Is it consuming unusual resources or making network connections?

These questions help turn a process listing into an investigation.

---

# 14. Key Takeaways

- A **process is a running program**.
- Every process has a **PID**.
- The **owner** tells you which account the process runs as.
- CPU and memory usage help identify unusual activity.
- A process has a **parent process** that can help explain how it started.
- Running processes can be inspected through **`/proc/<PID>`**.
- `ps aux` provides a **snapshot**.
- `top` provides a **live view**.
- High resource usage, unfamiliar processes, root ownership, unusual locations, and unexpected network activity are **clues**, not automatic proof of malware.
- `kill <PID>` can be used to terminate a process when appropriate.
- Processes are valuable **live evidence** during investigations.
- Process, network, and log evidence can be connected to build a larger picture.

## Final Takeaway

> **Processes are the heartbeat of a live Linux investigation.**

A file tells you what **could** happen.  
A process shows what is **happening now**.

The more you can see and understand about running processes, the less mysterious a live Linux system becomes.