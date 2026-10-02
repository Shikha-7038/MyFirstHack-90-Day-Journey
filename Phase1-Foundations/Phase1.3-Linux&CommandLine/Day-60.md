# Day 60 — Linux Software Management & Software Hygiene

## 📅 Day 60 of 90 — Linux Phase

### Topic
**Linux Software Management, APT & Software Hygiene**

---

## 1. Introduction

After learning how to investigate files, processes, network connections, and logs, the focus shifted from **investigating a system** to **maintaining a system securely**.

Every Linux system needs software to perform different tasks. That software needs to be installed, updated, removed when unnecessary, obtained from appropriate sources, and managed with awareness of what is installed.

This makes software management an important part of system security.

---

## 2. What Is a Package?

A **package** is a collection of files and information needed to install a piece of software on a Linux system.

A package can contain:

- Program files
- Dependencies
- Configuration files
- Documentation
- Metadata

Instead of manually finding every file and dependency required by a program, a package manager can handle much of this work.

---

## 3. What Is a Package Manager?

A **package manager** is a tool used to manage software packages on a Linux system.

On Ubuntu, one of the main package-management tools is:

**APT — Advanced Package Tool**

APT can be used to:

- Search for software
- Install software
- Update package information
- Upgrade installed software
- Remove software
- Manage dependencies

---

## 4. What Is a Repository?

A **repository** is a collection of software packages made available through configured software sources.

APT uses configured repositories to find and download packages.

This is important from a security perspective because **where software comes from matters**.

Using an appropriate, trusted software source provides more assurance than downloading an unknown installer from a random website. Software provenance and source trust still matter even when using a package manager.

---

## 5. APT and Software Management

The basic software-management workflow is:

**Search → Install → Use → Remove**

A broader security workflow is:

**Trusted Source → Package Manager → Install → Maintain → Remove When Unneeded**

This helps keep a system current, minimal, organized, and easier to understand.

---

## 6. `apt update`

```bash
sudo apt update
```

Refreshes the local package information from configured repositories.

It does **not** upgrade installed software. It refreshes the information APT uses to determine what updates are available.

---

## 7. `apt upgrade`

```bash
sudo apt upgrade
```

Installs available updates for installed packages when they can be upgraded through the normal upgrade process.

The normal sequence is:

```bash
sudo apt update
sudo apt upgrade
```

### Day 60 observation

The initial update check showed **57 packages could be upgraded**. After the upgrade, another update check showed **2 packages could still be upgraded**. This does not automatically mean the upgrade failed; some packages may require dependency changes or may be held back by the normal upgrade process.

---

## 8. Why Software Updates Matter for Security

When a vulnerability is discovered, developers may release an update containing a fix. However, the fix does not protect a system until the update is actually applied.

**Vulnerability discovered → Fix released → Update available → Update applied**

Until the update is applied, the vulnerable version may still be present. Once a vulnerability becomes publicly known, attackers can also study it and look for systems that have not applied the available fix.

> **A fix that hasn't been applied cannot protect the system.**

Keeping software updated is an important foundational security practice because it helps remove known, already-addressed weaknesses.

---

## 9. Viewing Installed Software

```bash
apt list --installed
```

The output contained **556 lines of package information**.

Examples included packages such as `vim`, `wget`, `wsl-pro-service`, `wsl-setup`, `zip`, `xz-utils`, and `zlib1g`.

Packages may appear as:

```text
[installed]
```

or:

```text
[installed,automatic]
```

`[installed,automatic]` generally means the package was installed automatically because another package depends on it.

---

## 10. Searching for Software

```bash
apt search cowsay
```

The search returned packages including:

```text
cowsay
cowsay-off
presentty
xcowsay
```

`apt search` is a **read-only operation**. It searches configured software sources but does not install anything.

---

## 11. Installing Software

```bash
sudo apt install cowsay
```

APT displayed information about the package, download size, disk space, source, installation progress, dependencies, and triggers.

The package was downloaded from the configured Ubuntu repository.

Package version used:

```text
3.03+dfsg2-8build1
```

Download size: approximately **18.1 kB**.

Disk space used: approximately **89.1 kB**.

---

## 12. Using the Installed Software

```bash
cowsay "Software hygiene matters"
```

The command displayed the message using the ASCII cow provided by `cowsay`.

The purpose of `cowsay` was not cybersecurity itself. It was a simple and harmless way to practice the complete software-management process.

---

## 13. Removing Software

```bash
sudo apt remove cowsay
```

The package was removed and approximately **89.1 kB** of space was freed.

This completed the practice cycle:

```text
Search → Install → Use → Remove
```

---

## 14. Software Provenance

Before installing software, it is useful to consider:

- Where did it come from?
- Who provides it?
- Is the source appropriate and trustworthy?
- What exactly will be installed?
- What changes will the installation make?

Using a configured repository through a package manager is generally preferable to blindly downloading an installer from an unknown website.

A random installer could potentially be modified, malicious, unwanted, or bundled with additional software.

> **Software source is part of the security decision.**

---

## 15. Be Careful With Installation Commands

A command such as:

```text
Just paste this into your terminal.
```

should not automatically be trusted.

Before executing an unfamiliar installation command, understand:

- Where the command came from
- What the command does
- What files it downloads
- What it changes
- What privileges it requires

This is especially important when a command uses `sudo`, because elevated privileges can allow significant system changes.

---

## 16. Connection With Day 56

Day 56 involved investigating a suspicious script without executing it.

**Day 56:** Observe → Analyze → Understand → Decide

The same mindset applies to software installation:

**Day 60:** Source → Understand → Verify → Execute

> **Don't blindly execute code just because it is available. Understand what you are trusting first.**

---

## 17. Software Hygiene

Software hygiene means maintaining software in a way that reduces unnecessary security and maintenance risks.

### 1. Keep software updated

Apply available security and software updates.

### 2. Use appropriate software sources

Consider the source and provenance of software before installing it.

### 3. Know what is installed

Unexpected or unknown software can become a security investigation clue.

### 4. Remove unnecessary software

Software that is no longer needed can contribute to unnecessary attack surface.

---

## 18. Security Connection

Software management is not only an administration task. It is also part of cybersecurity.

An outdated or unnecessary application can become part of the system's attack surface.

A security-conscious system therefore aims to keep software:

**Current + Trusted + Necessary**

This connects with least privilege:

- Least privilege reduces what users and processes are allowed to do.
- Software hygiene reduces what unnecessary or outdated software is present.

Both support the goal of reducing unnecessary risk.

---

## 19. Main Findings

During today's hands-on practice, I learned that:

- APT is used to manage software packages on Ubuntu.
- `apt update` refreshes package information.
- `apt upgrade` applies available package updates.
- `apt list --installed` shows installed packages.
- `apt search` can search configured repositories.
- `apt install` installs packages.
- `apt remove` removes packages.
- Package managers can handle dependencies and installation details.
- Software source and provenance matter.
- Updates can contain fixes for known vulnerabilities.
- A vulnerability remains relevant to an unpatched system even after a fix has been released.
- Unnecessary software can increase attack surface.
- Installation commands should not be executed blindly.

---

## 20. Key Lessons Learned

### Lesson 1 — Updating is a security practice

Keeping software current helps ensure that available security fixes are actually applied.

### Lesson 2 — Trust the source, not just the software name

Before installing something, consider where it came from and whether the source is appropriate.

### Lesson 3 — Know what is installed

Understanding the software present on a system makes it easier to maintain and investigate that system.

### Lesson 4 — Remove what you don't need

Unnecessary software can increase the system's attack surface.

### Lesson 5 — Don't blindly execute commands

An installation command can do much more than simply install a program. It may download files, execute code, modify configuration, or make other system changes.

---

## 21. Main Takeaway

> **Software hygiene means keeping software current, using appropriate trusted sources, knowing what is installed, and removing what is no longer needed.**

Today's `cowsay` exercise was simple, but it demonstrated an important cybersecurity principle:

**Installing software means trusting code.**

A secure mindset is not only about detecting malicious activity. It is also about making careful decisions **before software enters the system.**
