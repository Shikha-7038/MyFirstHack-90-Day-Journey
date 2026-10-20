# Day 64 — Linux System Hardening

## Overview

Day 64 focused on **Linux system hardening**: making a system more resistant to attacks by reducing unnecessary exposure, limiting privileges, protecting remote access, keeping software updated, and maintaining visibility through logging.

The main idea was:

> **Hardening is about reducing the attack surface before an incident happens.**

This day connected permissions, users and groups, software management, services, SSH, logging, and least privilege.

---

## 1. What Is System Hardening?

**System hardening** is the process of making a system more resistant to attacks by reducing unnecessary exposure and strengthening the components that remain.

Hardening is mainly **proactive**.

Instead of waiting for an incident and investigating what went wrong, hardening asks:

> How can I make the system harder to compromise before an attack happens?

A hardened system is not impossible to attack. The goal is to:

- Reduce unnecessary entry points
- Limit privileges
- Keep software updated
- Secure remote access
- Remove unnecessary services and software
- Monitor system activity
- Reduce the potential impact of a compromise

### Hardening vs Investigation

**Investigation** asks:

> What happened?

**Hardening** asks:

> What can I do to reduce the chance or impact of it happening?

A useful way to remember the difference:

**Investigation → Understand what went wrong**

**Hardening → Reduce what can go wrong**

---

## 2. Attack Surface

The **attack surface** is the collection of possible ways an attacker could interact with or attempt to compromise a system.

It can include:

- Network services
- Listening/open ports
- User accounts
- Privileged accounts
- Installed software
- Remote-access services
- Authentication mechanisms
- Unnecessary services
- Exposed interfaces

A larger attack surface can create more opportunities for attack. Removing unnecessary components and restricting access reduces those opportunities.

### Hardening mindset

A useful question is:

> **Does this need to be here, and if it does, how can it be made safer?**

This applies to services, accounts, software, privileges, ports, and remote access.

---

## 3. Core Hardening Actions

### Keep Software Updated

Check for available updates:

```bash
sudo apt update
```

This refreshes package information; it does **not** install updates.

To see available upgrades:

```bash
apt list --upgradable
```

During the assessment, **20 packages were listed as upgradable**, including packages associated with Ubuntu's security repository.

An available upgrade does not automatically mean it is a security fix. Updates can include security fixes, bug fixes, maintenance changes, or other improvements.

### Apply Least Privilege

Give users and processes only the permissions they actually need.

### Remove Unnecessary Components

Unused software, services, accounts, and network exposure can increase the attack surface.

### Secure Remote Access

SSH can provide powerful remote access, so authentication, key protection, and access restrictions matter.

### Monitor and Log

Prevention is not enough. Logs provide visibility and evidence for investigation.

---

# 4. Day 64 Hands-On Task — Harden-Assess Your Own System

The practical task was to assess the Linux system against a basic hardening checklist.

The assessment focused on **inspection and reasoning**, rather than aggressive configuration changes.

The task checked:

1. Software update status
2. Administrative access
3. Listening network services
4. SSH posture
5. Logging
6. Overall hardening priorities

---

## Step 1 — Check Software Update Status

### Commands

```bash
sudo apt update
apt list --upgradable
```

### Purpose

- Refresh package information
- Identify available updates
- Assess patching needs

### Result

The system reported:

```text
20 packages can be upgraded.
```

The upgrade list included packages associated with:

```text
resolute-updates
resolute-security
```

Examples included:

- `curl`
- `libcurl3t64-gnutls`
- `libcurl4t64`
- `libexpat1`
- `libglib2.0-*`
- `libxml2-16`
- `rsyslog`
- `sudo`

### Assessment

**Software updates need attention.**

`apt update` only refreshes package information. Updates can later be installed with:

```bash
sudo apt upgrade
```

---

## Step 2 — Check Accounts and Sudo Access

### Command

```bash
cat /etc/passwd
```

### Purpose

Inspect the accounts configured on the system.

The output contained the root account, system/service accounts, and the normal user account.

Many system/service accounts used restricted shells such as:

```text
/usr/sbin/nologin
```

or:

```text
/bin/false
```

These generally indicate that the accounts are not intended for normal interactive login.

### Check sudo access

```bash
getent group sudo
```

The result showed:

```text
sudo:x:27:shikha
```

This means the identified human user was a member of the `sudo` group.

### Assessment

There was **one identified human account with sudo access**.

The important question is:

> **Does each user with administrative access actually need it?**

This is the principle of **least privilege**.

---

## Step 3 — Check Listening Network Services

### Command

```bash
ss -tuln
```

### Purpose

Inspect listening TCP and UDP sockets.

Options:

- `-t` → TCP
- `-u` → UDP
- `-l` → listening sockets
- `-n` → numerical addresses and ports

The assessment showed activity involving:

- **Port 53** → DNS
- **Port 323** → time synchronization

Several listeners were bound to local/loopback interfaces.

### Important lesson

A listening port does **not automatically mean there is a vulnerability**.

For each listening service, ask:

- What service is using this port?
- Why is it listening?
- Does the service need to run?
- Does it need to be accessible beyond the local system?
- Can its exposure be reduced?

No services were disabled during the assessment.

---

## Step 4 — Check SSH Posture

### Command

```bash
ls -l ~/.ssh
```

The SSH directory contained an Ed25519 key pair:

```text
id_ed25519
id_ed25519.pub
```

The private key had restrictive permissions equivalent to:

```text
-rw-------
```

This means:

- Owner → read/write
- Group → no access
- Others → no access

The public key is designed to be shared with systems that should trust it for authentication.

### Assessment

The SSH private key had owner-only permissions.

This connected directly with Day 63:

> **Private authentication material should remain protected and accessible only to its owner.**

Having a key pair does not by itself prove that an SSH server is currently enabled or externally accessible.

---

## Step 5 — Check Logging

### Command

```bash
ls /var/log
```

The system contained several useful logging sources, including:

```text
auth.log
syslog
kern.log
dpkg.log
apt/
journal/
unattended-upgrades/
```

Examples:

- `auth.log` → authentication-related activity
- `syslog` → system and service events
- `kern.log` → kernel-related events
- `dpkg.log` → package-management activity
- `apt/` → package-management information
- `journal/` → systemd journal data where applicable

### Assessment

Logging was present, providing sources for monitoring and future investigation.

---

# 5. Mini Hardening Assessment

| Area | Finding | Assessment |
|---|---|---|
| Software updates | 20 packages upgradable | Updates need attention |
| Least privilege | 1 identified human account with sudo | Administrative access should remain necessary |
| Attack surface | Listening services identified with `ss -tuln` | Services should be understood and kept to what is needed |
| SSH | Ed25519 keys present; private key owner-only | Private-key permissions are appropriately restrictive |
| Monitoring | Multiple logs available | Logging provides visibility for investigation |

---

## One Thing to Harden First

The first thing identified for improvement was:

> **Address the pending software updates.**

The assessment found 20 available package upgrades, including packages associated with Ubuntu's security repository.

Keeping software updated helps reduce exposure to known vulnerabilities that have already received fixes.

The assessment and the actual change are separate:

**Assess → Understand → Apply the appropriate change**

---

# 6. Why “Reduce Attack Surface” Unifies Hardening

Most hardening actions connect to one central idea:

> **Reduce unnecessary opportunities for compromise.**

### Remove unnecessary software
Fewer components can mean fewer potential vulnerabilities.

### Remove unnecessary services
Fewer running services mean fewer potential entry points.

### Limit privileges
Fewer powerful accounts reduce the potential impact of account compromise.

### Restrict network exposure
Fewer accessible services reduce possible attack paths.

### Protect SSH
Secure authentication makes necessary remote access safer.

### Apply updates
Patching reduces exposure to known vulnerabilities.

### Monitor logs
Visibility helps identify and investigate suspicious activity.

---

# 7. Defence in Depth

**Defence in depth** means using multiple layers of protection instead of depending on one control.

For example:

```text
Secure SSH
     ↓
Least Privilege
     ↓
Updated Software
     ↓
Network Controls
     ↓
Logging & Monitoring
     ↓
Backups & Recovery
```

If one layer fails, other layers can still reduce the likelihood or impact of compromise.

This connects to:

- Network segmentation
- Zero Trust
- Least privilege
- Authentication
- Monitoring
- Incident investigation

---

# 8. Prevention, Detection, and Response

### Prevention

Hardening reduces unnecessary exposure.

Examples:

- Software updates
- Least privilege
- Secure SSH
- Reduced attack surface
- Removing unnecessary services

### Detection

Monitoring helps identify suspicious activity.

Examples:

- Authentication logs
- System logs
- Network monitoring
- Security alerts

### Response

Investigation helps determine what happened and what should happen next.

Examples:

- Process investigation
- File investigation
- Log analysis
- Network investigation
- Reconstructing events

A useful model is:

**Prevent → Detect → Investigate → Respond**

---

# 9. Key Takeaways

### 1. Hardening is proactive

Cybersecurity is not only about investigating incidents after they happen. Hardening reduces risk before an incident occurs.

### 2. Attack surface matters

Every unnecessary service, account, privilege, software component, or exposed network service can create additional opportunities for compromise.

### 3. Least privilege reduces impact

Users and processes should receive only the permissions they actually need.

### 4. Listening ports need context

A listening port is not automatically a vulnerability. It needs to be understood in terms of the service, configuration, and exposure.

### 5. Updates are part of security

Keeping software updated helps reduce exposure to known vulnerabilities.

### 6. SSH requires careful protection

Remote access is powerful, so authentication and private-key permissions matter.

### 7. Logging supports security

Prevention and monitoring work together. Logs provide evidence when something needs to be investigated.

### 8. Hardening is about reduction

The goal is not to make a system perfectly secure.

The goal is to make unnecessary compromise opportunities fewer, make successful compromise harder or less damaging, and improve the ability to detect what happens.

---

# 10. Final Day 64 Summary

The biggest lesson from Day 64 was:

> **Hardening is not about adding security everywhere. It is about reducing unnecessary exposure and protecting what remains.**

A useful mental model is:

**Assess → Reduce → Protect → Monitor**

- **Assess** what exists.
- **Reduce** unnecessary exposure.
- **Protect** the access and services that need to remain.
- **Monitor** activity so problems can be detected and investigated.

Day 64 brought together many Linux concepts learned throughout this phase:

**Users → Permissions → Privileges → Processes → Services → Logs → SSH → Updates → Hardening**

This creates the foundation for the next step: investigating a compromised Linux system and reconstructing what happened.
