# Day 48 — Linux Filesystem

## MyFirstHack 90-Day Cybersecurity Journey

**Day:** 48/90  
**Topic:** Linux Filesystem  
**Environment:** Ubuntu 26.04 LTS on WSL2  
**Lab Type:** Read-only filesystem exploration

---

## 1. Objective

The goal of Day 48 was to understand how Linux organizes its filesystem and to explore that structure in a real Ubuntu environment.

The main concepts covered were:

- The Linux filesystem as one unified tree
- The root directory `/`
- Important standard directories
- Absolute and relative paths
- Special path symbols: `.`, `..`, and `~`
- The concept that nearly everything is treated through a file-like interface
- Why these concepts matter during Linux security investigations

---

## 2. Linux Filesystem Structure

Linux organizes files and directories into a **single unified filesystem tree**.

A simplified view is:

```text
/
├── home
├── etc
├── var
│   └── log
├── tmp
├── dev
├── proc
├── usr
└── root
```

The top of the tree is the **root directory**:

```text
/
```

Unlike Windows, where drives such as `C:` and `D:` normally represent separate drive trees, Linux presents the filesystem under one root. Additional storage can be attached to this tree through mount points.

### Important distinction

- `/` = root **directory**
- `root` = highly privileged administrative **user**

They are different concepts.

---

## 3. Important Linux Directories

| Directory | Purpose | Cybersecurity Relevance |
|---|---|---|
| `/home` | Personal directories for regular users | User files and activity |
| `/etc` | System configuration files | Security settings and configuration |
| `/var` | Variable/changing system data | Logs and other runtime data |
| `/var/log` | System and application logs | Security investigation and incident analysis |
| `/tmp` | Temporary files | Can contain temporary or suspicious artifacts |
| `/dev` | Device entries | Hardware and device interfaces |
| `/proc` | Process and live system information | Investigating running processes and system state |
| `/usr` | Programs and supporting system resources | Software and commands |
| `/bin` | Essential command-line programs | Basic system utilities |
| `/sbin` | System administration programs | Administrative utilities |
| `/root` | Home directory of the root user | Administrator files |

> Modern Linux distributions may integrate `/bin` and `/sbin` with corresponding directories under `/usr`.

### Security-focused directories

Remember these especially:

```text
/etc
→ Configuration

/var/log
→ Logs

/tmp
→ Temporary files

/dev
→ Devices

/proc
→ Processes and live system information
```

---

## 4. Absolute Paths

An **absolute path** gives the complete route from the root directory.

It always begins with `/`.

Example:

```text
/home/user/documents/report.txt
```

The route is:

```text
/
└── home
    └── user
        └── documents
            └── report.txt
```

An absolute path is unambiguous and does not depend on the current directory.

> **Absolute path = full address**

Example:

```bash
cd /var/log
```

---

## 5. Relative Paths

A **relative path** starts from the current directory.

It does not begin with `/`.

If the current directory is:

```text
/home/user
```

then:

```text
documents/report.txt
```

means:

```text
/home/user/documents/report.txt
```

The meaning of a relative path depends on the current location.

> **Relative path = directions from where I am**

---

## 6. Special Path Symbols

### `.` — Current Directory

```text
.
```

means the directory you are currently in.

### `..` — Parent Directory

```text
..
```

means the parent directory, one level above the current location.

If the current directory is:

```text
/home/user/documents
```

then:

```text
..
```

refers to:

```text
/home/user
```

And:

```text
../..
```

refers to:

```text
/home
```

### `~` — Home Directory

The tilde represents the current user's home directory, typically:

```text
/home/your-username
```

---

## 7. `pwd` — Print Working Directory

```bash
pwd
```

means **Print Working Directory**.

It displays the absolute path of your current location.

Example:

```text
/home/your-username
```

This is useful before using relative paths because it tells you where you currently are.

---

## 8. `ls` — List Directory Contents

```bash
ls
```

lists the contents of a directory.

Examples used during the lab:

```bash
ls /
ls /etc
ls /var/log
ls /tmp
ls /dev
```

These commands were used only to observe the filesystem.

---

# 9. "Nearly Everything Is a File"

One of Linux's distinctive ideas is that **nearly everything is treated through a file-like interface**.

This does not mean every system component is literally an ordinary text file.

Linux exposes many resources through files, special files, or virtual filesystems.

Examples:

```text
/dev
→ Device interfaces

/proc
→ Processes and live system information

/etc
→ Configuration

/var/log
→ Logs
```

This provides a consistent way for programs and users to interact with many parts of the system.

---

## 10. Why This Matters in Cybersecurity

Linux security investigations often involve finding and reading the right information.

For example:

```text
/etc
↓
Inspect configuration

/var/log
↓
Investigate events and activity

/proc
↓
Inspect running processes and live system information

/tmp
↓
Look for suspicious temporary artifacts

/dev
↓
Understand devices
```

This leads to an important cybersecurity mindset:

> **A large part of Linux investigation is knowing where to look and what to read.**

---

# 11. Practical Lab — Explore the Linux Tree

The Day 48 practical task was a **read-only exploration** of Ubuntu.

### Step 1 — Find where you are

```bash
pwd
```

This showed the current working directory, which was the Linux home directory.

### Step 2 — See the top of the tree

```bash
ls /
```

This displayed the top-level directories.

### Step 3 — Explore configuration

```bash
ls /etc
```

This displayed system configuration files and directories.

### Step 4 — Explore logs

```bash
ls /var/log
```

This displayed Linux log files and log-related directories.

### Step 5 — Explore temporary files

```bash
ls /tmp
```

This displayed the contents of the temporary-file directory.

### Step 6 — Explore devices

```bash
ls /dev
```

This displayed device entries and demonstrated the file-like interface concept.

No files were modified during the lab.

---

# 12. Absolute vs Relative Path

| Feature | Absolute Path | Relative Path |
|---|---|---|
| Starting point | Root `/` | Current directory |
| Begins with `/` | Yes | No |
| Depends on current location | No | Yes |
| Example | `/var/log` | `../logs` |
| Mental model | Full address | Directions from here |

### Simple rule

> **Absolute starts from root. Relative starts from where you are.**

---

# 13. Day 48 Command Cheat Sheet

```bash
pwd
```

Show the current directory.

```bash
ls /
```

List the root directory.

```bash
ls /etc
```

Explore system configuration.

```bash
ls /var/log
```

Explore Linux logs.

```bash
ls /tmp
```

Explore temporary files.

```bash
ls /dev
```

Explore device entries.

---

# 14. Key Takeaways

- Linux organizes its filesystem as **one unified tree** beginning at `/`.
- `/` is the root directory; it is different from the `root` user.
- Absolute paths begin with `/` and give the complete route.
- Relative paths begin from the current directory.
- `.` means the current directory.
- `..` means the parent directory.
- `~` means the current user's home directory.
- `/etc` contains configuration.
- `/var/log` contains logs.
- `/tmp` contains temporary files.
- `/dev` exposes device interfaces.
- `/proc` exposes processes and live system information.
- Nearly everything is treated through a file-like interface, making file-handling skills useful across much of Linux.

---

# 15. Cybersecurity Connection

Filesystem knowledge is an important foundation for Linux security work.

A security analyst may need to locate:

- Configuration
- Logs
- User files
- Running processes
- Temporary artifacts
- Device information
- Other system state

The key mindset is:

> **Know where Linux stores information, then know how to read it.**

This becomes especially useful in later Linux investigations and the Day 65 compromised-system capstone.

---

# 16. Personal Learning Summary

Today I moved from learning the Linux filesystem conceptually to actually exploring it in Ubuntu.

I used:

```bash
pwd
ls /
ls /etc
ls /var/log
ls /tmp
ls /dev
```

The biggest realization was that Linux is not simply a collection of folders. It is an organized filesystem tree that provides access to many different parts of the system.

The most important lesson I am taking forward is:

> **Before investigating a Linux system, I need to understand where information lives and how to reach it.**

---

## Day 48 Status

**COMPLETE ✅**

### Skills Practiced

- [x] Understand the Linux filesystem tree
- [x] Understand the root directory `/`
- [x] Identify important Linux directories
- [x] Understand absolute paths
- [x] Understand relative paths
- [x] Understand `.`, `..`, and `~`
- [x] Use `pwd`
- [x] Use `ls`
- [x] Explore `/etc`
- [x] Explore `/var/log`
- [x] Explore `/tmp`
- [x] Explore `/dev`
- [x] Connect filesystem knowledge to cybersecurity investigation

---

## What's Next?

**Day 49 — Linux Navigation**

The next step is to start navigating through the filesystem confidently using Linux commands such as `cd`, `ls`, and `pwd`.
