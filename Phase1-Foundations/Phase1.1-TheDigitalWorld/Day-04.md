# Day 4 – How Computers Actually Work

**Date:** July 27, 2026

## 🎯 Objective

The objective of Day 4 was to understand how a computer actually works internally before diving deeper into cybersecurity. Rather than simply knowing how to use a computer, today's goal was to understand what happens behind the scenes whenever an application is opened, how the operating system manages resources, and why this knowledge is important from a cybersecurity perspective.

---

# 📚 Topics Covered

- Computer Components
- CPU (Central Processing Unit)
- RAM (Random Access Memory)
- Storage (HDD / SSD)
- Input and Output Devices
- Operating System
- Kernel Space vs User Space
- Process Management
- Memory Management
- CPU Vulnerabilities
- Process Monitoring
- Why Attackers Target Memory

---

# 🖥️ Understanding the Core Components of a Computer

## 1. CPU (Central Processing Unit)

The CPU is responsible for executing instructions and performing calculations. Every application running on a computer ultimately depends on the CPU to execute its instructions.

I learned that the CPU does **not** directly read programs from storage. Instead:

1. The program is loaded from storage.
2. It is copied into RAM.
3. The CPU executes instructions from RAM because RAM is much faster than storage.

---

## 2. RAM (Random Access Memory)

RAM acts as the computer's temporary working memory.

Whenever an application is opened:

1. The application is read from storage.
2. It is loaded into RAM.
3. The CPU begins executing instructions from RAM.

### Characteristics

- Temporary storage
- Very fast
- Stores running applications
- Data disappears when the computer shuts down

One important cybersecurity lesson was that sensitive information such as passwords, authentication tokens, and encryption keys may temporarily exist inside RAM while applications are running.

---

## 3. Storage

Storage permanently keeps:

- Operating System
- Applications
- Documents
- Images
- Videos
- Configuration files

Unlike RAM, storage retains its contents even after shutting down the computer.

---

## 4. Input and Output Devices

### Input Devices

Devices that send information to the computer.

Examples:

- Keyboard
- Mouse
- Webcam
- Microphone

### Output Devices

Devices that display results from the computer.

Examples:

- Monitor
- Printer
- Speakers

---

# ⚙️ How a Program Actually Runs

Before today's lesson, I simply clicked an application without thinking about what happened internally.

Now I understand the complete flow:

```text
Storage
   ↓
RAM
   ↓
CPU
   ↓
Output Device
```

This sequence helped me understand why computers with insufficient RAM become slow even if they have fast processors.

---

# 🖥️ Operating System

The Operating System acts as the manager of all hardware resources.

Its responsibilities include:

- Process Management
- Memory Management
- Device Management
- File Management
- User Management

Without an operating system, applications cannot safely communicate with hardware.

---

# 🔒 Kernel Space vs User Space

## User Space

Applications like:

- Chrome
- VS Code
- Spotify

run inside User Space with limited permissions.

---

## Kernel Space

The Kernel has unrestricted access to:

- CPU
- RAM
- Storage
- Hardware devices

Because the Kernel controls everything, any vulnerability inside it can affect the entire operating system.

---

# 💡 Why This Separation Matters

One question I explored after the lesson was:

> **Why don't all applications simply run with full permissions?**

I learned that allowing every application unrestricted access would make malware far more dangerous.

Separating User Space from Kernel Space creates an important security boundary that prevents applications from directly accessing critical operating system resources.

---

# ⚡ Process Management

A process is simply a running program.

Examples include:

- Chrome
- VS Code
- Microsoft Word

Modern computers often have hundreds of running processes simultaneously.

The operating system continuously:

- Creates processes
- Schedules CPU time
- Allocates memory
- Terminates finished processes

Understanding processes is important because attackers often disguise malware as legitimate Windows processes.

---

# 🧠 Memory Management

The operating system assigns separate memory regions to each running application.

This prevents applications from reading or modifying another application's memory.

Without memory management:

- Programs could overwrite each other.
- Sensitive information could easily leak.
- Malware would have unrestricted access to every running application.

---

# 🚨 CPU Vulnerabilities

I also learned that hardware itself can contain vulnerabilities.

Two famous examples are:

- Spectre
- Meltdown

These attacks exploited CPU optimizations rather than software bugs.

This changed my understanding because I previously assumed cybersecurity was only about protecting software.

---

# 🔍 Process Monitoring

Another interesting topic was process monitoring.

I learned about attacks where malware changes only one character in its filename.

Legitimate process:

```text
svchost.exe
```

Malicious process:

```text
svch0st.exe
```

The attacker replaces the letter **o** with the number **0**.

At first glance, both names appear identical.

This type of deception is called a **Homoglyph Attack**.

It showed me why security analysts carefully inspect running processes rather than trusting filenames.

---

# 🛠️ Practical Task Completed

Today's practical task involved observing how applications run on a computer and understanding that every application becomes a process managed by the operating system.

I also explored how Windows manages processes and why monitoring them is an important part of cybersecurity.

Instead of simply memorizing the theory, I connected each computer component with its practical role during everyday computer usage.

---

# ❓ Questions I Explored Beyond the Lesson

## Why is RAM important in cybersecurity?

I learned that RAM does not only improve performance.

Sensitive information such as:

- Passwords
- Authentication tokens
- Encryption keys

may temporarily exist inside memory while applications are running.

This explains why attackers sometimes perform **memory dumping attacks** and why Digital Forensics and Incident Response (DFIR) teams often analyze RAM.

---

## Why do attackers target memory instead of storage?

Storage usually contains encrypted or protected files.

Memory, however, may temporarily contain decrypted information that applications are actively using.

Because of this, RAM can provide attackers with valuable information that never exists on disk in plain text.

---

## Why are Kernel Space and User Space separated?

Initially, I assumed every application could directly communicate with hardware.

After learning about operating system architecture, I understood that this separation prevents applications from accidentally or intentionally damaging the operating system.

This design greatly improves both security and system stability.

---

## Why do attackers rename malware to look like legitimate processes?

I learned that many users only glance at filenames.

By changing a single character, attackers can trick users into believing malicious software is actually a legitimate Windows process.

This reinforced the importance of careful process monitoring.

---

# 📌 My Findings

## Finding 1

Before today, I thought applications simply "opened" when clicked.

Now I understand that every application follows this sequence:

```text
Storage → RAM → CPU → Output Device
```

The CPU never executes programs directly from storage.

---

## Finding 2

I realized RAM is not just used to improve performance.

It temporarily contains valuable information such as passwords, authentication tokens, and encryption keys.

This explains why attackers often target memory during advanced attacks.

---

## Finding 3

I understood why User Space and Kernel Space exist.

Giving every application full hardware access would make malware much more dangerous and could easily crash the operating system.

The separation acts as an important security boundary.

---

## Finding 4

One surprising lesson was that malware does not always look suspicious.

Sometimes attackers simply rename malicious files so they closely resemble legitimate system processes.

A tiny character difference can easily fool users who are not paying attention.

---

# ✅ Key Takeaways

- The CPU executes instructions from RAM, not directly from storage.
- RAM temporarily stores running applications and sensitive information.
- Storage permanently stores files and programs.
- The Operating System manages all hardware resources.
- User Space and Kernel Space provide an important security boundary.
- Every running application is a process managed by the operating system.
- Hardware vulnerabilities like Spectre and Meltdown show that cybersecurity extends beyond software.
- Memory analysis is an important technique in Digital Forensics and Incident Response (DFIR).
- Process monitoring helps detect suspicious or disguised malware.

---

# 💭 Personal Reflection

Before today, I mainly focused on learning cybersecurity tools and attacks. This lesson showed me that understanding how a computer works internally is equally important.

I realized that concepts like RAM, CPU, processes, and the operating system are not just theoretical topics—they explain why many cyberattacks succeed and how defenders investigate them.

Today's lesson gave me a much stronger foundation for understanding future topics such as malware analysis, operating systems, digital forensics, and incident response.

---

# 🚀 End of Day 4

Today laid the foundation for understanding how computers operate internally. This knowledge will support future topics in networking, operating systems, malware analysis, digital forensics, and incident response throughout my cybersecurity learning journey.