# Day 47 — Setting Up My Linux Environment

**MyFirstHack 90-Day Cybersecurity Journey**  
**Phase:** Linux & Command Line  
**Day:** 47  
**Topic:** Setting Up My Linux Environment

---

## 1. Objective

The goal of Day 47 was to move from **reading about Linux to actually using Linux**.

For cybersecurity, Linux is important because it is widely used in servers, cloud infrastructure, networking, system administration, and security operations.

The objective was not to become a Linux expert immediately, but to build enough command-line comfort to navigate and investigate Linux systems without feeling lost in the terminal.

---

## 2. Why Linux Matters in Cybersecurity

Linux is commonly used in:

- Servers
- Cloud infrastructure
- Networking
- Security tools
- System administration
- Cybersecurity investigations

Learning the Linux command line is therefore an important foundation for future cybersecurity work.

---

## 3. Ways to Run Linux

There are several ways to use Linux:

### WSL — Windows Subsystem for Linux
Runs a Linux environment directly alongside Windows.

**Advantages:**
- Easy to use on Windows
- Fast and lightweight
- Good integration with Windows
- Excellent for command-line practice

### Virtual Machine
Runs Linux inside a virtual computer using software such as VirtualBox.

**Advantages:**
- More complete Linux experience
- Stronger separation from the host than WSL in many situations

**Trade-off:** It generally requires more RAM and storage.

### Cloud / Browser
Provides access to a Linux environment remotely without installing it locally.

### Dual Boot
Installs Linux alongside Windows and lets the user choose the operating system when starting the computer.

---

## 4. Ubuntu vs Kali Linux

### Ubuntu

Ubuntu is a general-purpose Linux distribution and is beginner-friendly.

It is useful for:

- Learning Linux fundamentals
- Practicing command-line skills
- General system administration
- Server and development work

### Kali Linux

Kali Linux is a security-focused Linux distribution containing many tools used for penetration testing and security work.

### Key Lesson

**Learn Linux fundamentals first → specialise with security tools later.**

The basic Linux command-line skills learned in Ubuntu transfer to Kali and many other Linux distributions.

---

## 5. WSL 2 Setup

The Linux environment for this phase was set up using:

**Windows → WSL 2 → Ubuntu 26.04 LTS → Linux Terminal**

During setup, the initial installation attempts returned a:

`403 Forbidden`

error.

Instead of stopping, the installation was completed using a more manual setup process.

The required Windows features were enabled:

- `Microsoft-Windows-Subsystem-Linux`
- `VirtualMachinePlatform`

After restarting and updating WSL, Ubuntu was installed successfully.

---

## 6. Ubuntu 26.04 LTS

The selected distribution was:

**Ubuntu 26.04 LTS**

LTS means **Long-Term Support**.

Ubuntu was selected because the focus of this phase is learning Linux fundamentals and command-line skills rather than immediately using a specialised security distribution.

---

## 7. Understanding the Linux Terminal

A typical Linux prompt can look like:

```text
student@linux:~$
```

Each part has meaning:

- `student` → current Linux username
- `linux` → computer/host name
- `~` → current user's home directory
- `$` → shell is ready for a normal user's command

The Linux environment has its own Linux user context. Linux passwords also behave differently from normal graphical password fields: when typing a password in the terminal, characters normally do not appear on screen.

---

## 8. Linux Home Directory

The home directory is the user's personal working area.

Example:

```text
/home/student
```

The shortcut:

```text
~
```

represents the current user's home directory.

To move to it:

```bash
cd ~
```

To check the current location:

```bash
pwd
```

---

## 9. Commands Practiced

### `whoami`

Shows the current Linux user.

```bash
whoami
```

Example output:

```text
student
```

**Purpose:** Helps identify which account is currently being used.

---

### `pwd`

Means **Print Working Directory**.

```bash
pwd
```

Example output:

```text
/home/student
```

**Purpose:** Shows the directory where you are currently working.

---

### `uname -a`

Displays Linux system and kernel information.

```bash
uname -a
```

It can show information such as:

- Kernel name
- Hostname
- Kernel version
- System architecture

The output from the environment confirmed that it was running under **WSL2**.

---

### `echo`

Displays text in the terminal.

```bash
echo "Hello Linux"
```

Output:

```text
Hello Linux
```

**Purpose:** Demonstrates the basic relationship between a command and its output.

---

### `cd`

Means **change directory**.

Example:

```bash
cd ~
```

**Purpose:** Moves between directories.

---

## 10. Verification

After installation, the Linux environment was verified using:

```bash
cd ~
pwd
whoami
uname -a
echo "Hello Linux"
```

The checks confirmed:

- The home directory was accessible
- The Linux user was recognised
- Linux/kernel information was available
- WSL2 was running
- Commands were executing successfully

---

## 11. Troubleshooting Experience

The setup did not work on the first attempt.

The troubleshooting process was:

```text
WSL installation attempt
        ↓
403 Forbidden error
        ↓
Investigate the problem
        ↓
Enable required Windows features
        ↓
Restart Windows
        ↓
Install/update WSL 2
        ↓
Install Ubuntu
        ↓
Verify Linux environment
```

### Lesson

**Troubleshooting is part of technical work.**

A failed command is not necessarily the end of the task. Understanding the error, finding the correct solution, and verifying the result are valuable technical skills.

---

## 12. Important WSL Note

WSL is a controlled Linux environment integrated with Windows, but it should **not** be treated as a completely isolated sandbox.

WSL can interact with Windows resources and files. Therefore, commands should still be used carefully.

A traditional virtual machine can provide stronger separation from the host in many configurations, but no environment should be treated as completely risk-free.

---

## 13. Why These Basic Commands Matter for Cybersecurity

The commands practiced on Day 47 are simple, but they establish the foundation for later investigation.

For example:

```bash
whoami
```

helps determine **who you are operating as**.

```bash
pwd
```

helps determine **where you are**.

```bash
uname -a
```

helps determine **what system you are working with**.

These concepts become useful later when:

- Investigating suspicious files
- Examining system logs
- Checking running processes
- Investigating network activity
- Understanding permissions
- Investigating compromised Linux systems

---

## 14. Key Learnings

By completing Day 47, I learned:

1. Why Linux is important in cybersecurity.
2. Different ways to run Linux.
3. What WSL and WSL2 are.
4. Why Ubuntu was chosen for Linux fundamentals.
5. The difference between Ubuntu and Kali Linux.
6. How to read a Linux terminal prompt.
7. What `~` means.
8. How to move to the home directory.
9. How to identify the current Linux user.
10. How to identify the current directory.
11. How to check Linux/kernel information.
12. How to execute basic Linux commands.
13. How to troubleshoot a WSL installation problem.
14. Why command-line skills are important for cybersecurity.

---

## 15. Practical Outcome

**Day 47 was successfully completed.**

The Linux environment is now ready for the rest of the Linux & Command Line phase.

The working environment is:

```text
Windows
   ↓
WSL 2
   ↓
Ubuntu 26.04 LTS
   ↓
Linux Terminal
   ↓
Command-Line Practice
```

---

## 16. Key Takeaway

> **Linux is not just another operating system to learn. For cybersecurity, understanding the command line provides a foundation for exploring, troubleshooting, and investigating systems.**

---

## 17. Next Step

**Day 48 — The Linux Filesystem**

Next topic:

> **“Nearly everything is a file.”**

The next lesson will focus on understanding the Linux filesystem, directories, paths, and how Linux organizes information.

---

**Status: Day 47 Complete ✓**
