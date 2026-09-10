# Day 46 — Linux & Command Line: The Foundation of Cybersecurity

**MyFirstHack 90-Day Cybersecurity Journey**  
**Phase:** Linux & Command Line  
**Day:** 46/90

---

## 1. Overview

Day 46 marked the beginning of a new phase of my cybersecurity journey: **Linux and the Command Line**.

After completing the Networks phase, this phase focuses on learning how to directly interact with and investigate computer systems using Linux and command-line tools.

The goal is not to become a Linux expert. The goal is to develop enough command-line confidence to navigate a Linux system, work with files, understand permissions, investigate processes and logs, automate tasks, connect to remote systems, and eventually investigate a compromised Linux machine.

---

## 2. What is Linux?

Linux is an **operating system**, just like Windows and macOS.

An operating system acts as the layer between computer hardware and applications. It manages system resources and provides an environment in which applications can run.

Linux is different from many traditional operating systems because it is **open source**. Its source code is available for people to inspect, modify, and improve according to its license.

Linux is also available in many different **distributions (distros)**.

Examples include:

- Ubuntu — beginner-friendly and widely used
- Debian — known for stability
- Fedora — modern Linux distribution
- Kali Linux — designed for security testing

These distributions can have different tools and interfaces, but they share the Linux kernel at their core.

---

## 3. Why Linux is Important in Cybersecurity

Linux is heavily used in cybersecurity because it is widely present in the infrastructure that security professionals work with.

### Servers and Cloud Infrastructure

Many web servers, application servers, backend systems, and cloud environments use Linux.

This means cybersecurity professionals may need to investigate and secure Linux systems as part of their work.

### Security Tools

Many security tools are available on Linux or are commonly used from Linux environments.

Examples include:

- Wireshark
- Snort
- Suricata
- Zeek
- Kali Linux security tools

### Network Infrastructure

Linux is also used in many network and infrastructure environments.

Understanding Linux therefore helps when investigating network activity, services, system configurations, and connections.

### Investigation

Security professionals may need to examine:

- Files
- Users
- Permissions
- Processes
- Network connections
- System logs

Linux provides command-line tools that make this information accessible for investigation.

---

## 4. What is the Command Line?

The **command line**, also called the **Command-Line Interface (CLI)**, is a way of interacting with a computer by typing commands instead of primarily using graphical menus and buttons.

The basic process is:

**Type a command → Press Enter → System executes it → Result is displayed**

For example:

```text
whoami
```

The command asks the system to display the username of the current user.

The terminal provides an interface for entering these commands, while a **shell** interprets the commands and communicates with the operating system.

---

## 5. Why Cybersecurity Uses the Command Line

### Precision

The command line allows users to give the system very specific instructions.

Instead of navigating through several graphical menus, a command can directly perform a particular operation.

### Combination

Command-line tools can be connected together so that the output from one command can be processed by another.

This allows small, focused commands to be combined into more powerful operations.

This concept will become especially important when learning **pipes**.

### Automation

Commands can be saved into scripts and executed automatically.

This is useful for repetitive cybersecurity tasks such as:

- Searching logs
- Checking systems
- Processing files
- Gathering information
- Performing repeated investigation tasks

### Speed

Once commands become familiar, many technical tasks can be performed faster than navigating through graphical interfaces.

### Remote Access

Command-line environments work extremely well for remote administration.

Using **SSH (Secure Shell)**, a security professional or administrator can connect to a remote Linux machine and work with it through the terminal.

This is important because servers are often located somewhere else and may not have a graphical interface available.

---

## 6. Command Line vs Graphical Interface

| Graphical Interface | Command Line |
|---|---|
| Uses buttons, windows and menus | Uses typed commands |
| Easier for beginners | Requires learning commands |
| Options are visible | Commands must be known or looked up |
| Good for visual tasks | Powerful for technical tasks |
| Can require many clicks | Can perform tasks quickly |
| Less convenient for automation | Excellent for scripting |
| Usually requires graphical access | Works well over remote connections |

The command line is not necessarily better for every task. Its main advantage is the **control, flexibility, and automation** it provides for technical work.

---

## 7. Why Linux Fits Cybersecurity Investigation

Cybersecurity investigations often require answering questions such as:

- **Who** performed an action?
- **What** happened?
- **When** did it happen?
- **Which files or processes** were involved?
- **Which network connections** were made?
- **What do the logs show?**
- **Who has permission** to access something?

Linux provides tools and system information that can help answer these questions.

This makes command-line knowledge particularly valuable for security analysts, system administrators, penetration testers, incident responders, and other cybersecurity professionals.

---

## 8. Connection With My Previous Networking Phase

The Linux phase directly builds on what I learned during the Networks phase.

### Networks

I learned **how systems communicate**.

### Logs

I learned **what systems record**.

### Forensics

I learned **how evidence can be used to reconstruct events**.

### Linux

I will now learn **how to directly interact with and investigate the systems involved**.

This means Linux is not a separate detour from cybersecurity. It provides a practical environment where many of the concepts I have already learned can be applied.

---

## 9. Linux is Already Around Us

Linux is not limited to personal computers.

It is commonly used in:

- Web servers
- Cloud infrastructure
- Network devices
- Android devices
- Embedded systems
- Smart devices
- Security infrastructure

Much of Linux's presence is hidden behind the applications and services people use every day.

---

## 10. My Starting Relationship With the Command Line

The command line feels familiar to me because I have previously used it while working with virtual machines in Oracle VirtualBox and have performed various commands.

However, this phase will help me move beyond simply running commands and develop a deeper understanding of **what the commands do, why they are useful, and how they can be applied to cybersecurity tasks**.

---

## 11. Linux Phase Roadmap

The upcoming lessons will gradually build Linux and command-line skills.

**Linux environment**  
↓  
**Filesystem**  
↓  
**Navigation**  
↓  
**Files**  
↓  
**Users and permissions**  
↓  
**Searching and combining commands**  
↓  
**Suspicious-file investigation**  
↓  
**Processes**  
↓  
**Networking**  
↓  
**System logs**  
↓  
**Software management**  
↓  
**Bash scripting**  
↓  
**Scheduled tasks**  
↓  
**SSH**  
↓  
**Linux hardening**  
↓  
**Compromised Linux system investigation**

---

## 12. Key Terms Learned

### Linux
An operating system built around the Linux kernel.

### Kernel
The core part of an operating system that manages communication between software and hardware.

### Open Source
Software whose source code is available to inspect, modify, and redistribute according to its license.

### Distribution / Distro
A complete Linux operating system package built around the Linux kernel.

### Terminal
An application/interface used to interact with a computer, commonly through commands.

### CLI
Command-Line Interface; an interface where users interact with a system by typing commands.

### Shell
A program that interprets commands and communicates with the operating system.

### SSH
Secure Shell; a protocol commonly used to securely access remote systems through a command-line interface.

### Bash
A popular Unix/Linux shell and scripting environment.

---

## 13. Key Takeaways

1. Linux is an **operating system**, like Windows and macOS.
2. Linux is **open source** and is available through many distributions.
3. Linux is widely used in **servers, cloud infrastructure, networking, and security environments**.
4. The command line allows users to interact with a computer by **typing commands**.
5. Command-line skills provide **precision, flexibility, automation, speed, and remote access**.
6. Linux command-line knowledge is useful for **security investigation and system administration**.
7. The command line has a learning curve, but familiarity develops through practice.
8. The objective of this phase is not to memorize every Linux command but to understand **how to interact with and investigate a Linux system**.
9. Linux connects directly with the networking, logging, and forensic concepts learned in the previous phase.
10. The final goal is to become comfortable enough with Linux to **investigate a compromised system**.

---

## 14. Final Reflection

Day 46 introduced Linux and the command line as the foundation for the next stage of my cybersecurity learning.

The most important thing I learned is that Linux is not simply another operating system to study. It is an environment widely used by the systems, servers, infrastructure, and security tools that cybersecurity professionals work with.

The command line may initially seem less friendly than a graphical interface, but it provides direct control, automation, and powerful ways to investigate systems.

My goal for this phase is simple:

> **Become comfortable enough with the Linux terminal to understand what is happening on a system and know how to investigate it.**

**Day 46 completed — Linux & Command Line phase started.**