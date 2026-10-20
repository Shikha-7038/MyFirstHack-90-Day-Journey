# Day 63 — SSH: Remote Access, Authentication & Security 🔐🐧

## Overview

Today I learned how **SSH (Secure Shell)** allows users and security professionals to securely access and manage Linux systems remotely.

Until now, many of my Linux activities were performed directly on my local Ubuntu environment. SSH showed me how those same command-line and investigation skills can be extended to another machine over a network.

I also learned why SSH is both an essential administration tool and an important security target.

---

# What is SSH?

**SSH (Secure Shell)** is a protocol used to securely connect to and control a remote computer over a network.

With SSH, I can interact with a remote Linux system through a command-line interface without physically being in front of that machine.

For example:

```bash
ssh username@server_address
```

After authentication, commands entered into the terminal are executed on the remote machine and their results are returned to the local terminal.

When finished, the remote session can be closed with:

```bash
exit
```

or:

```bash
logout
```

---

# Why SSH Matters in Cybersecurity

Security professionals often need to work with systems that are not physically nearby.

A server may be:

- In a data centre
- In another building
- In another city or country
- Hosted in the cloud
- Part of an organization's internal infrastructure

SSH makes it possible to securely access these systems from another location.

It is commonly used by:

- System administrators
- SOC analysts
- Security engineers
- Incident responders
- Linux administrators

SSH also extends the usefulness of Linux skills such as:

- Command-line navigation
- Process inspection
- Log analysis
- File management
- Network investigation
- Scripting
- System administration

---

# SSH Client-Server Model

SSH uses a **client-server model**.

```text
Local Machine
SSH Client
     |
     | Encrypted SSH connection
     |
     v
Remote Linux Machine
SSH Server
```

### SSH Client

The client runs on the machine from which I initiate the connection.

Example:

```bash
ssh username@server_address
```

### SSH Server

The remote machine runs an SSH server that listens for incoming SSH connections.

SSH commonly uses:

```text
Port 22
```

This connects with the networking concept of **ports** learned earlier in the journey.

---

# Encryption in SSH

SSH encrypts communication between the client and server.

This helps protect information such as:

- Commands
- Command output
- Authentication information
- Other data transferred during the session

Without secure encryption, sensitive information sent over a network could potentially be observed by someone monitoring the communication.

SSH replaced older insecure remote-access approaches that transmitted information without adequate protection.

---

# SSH Authentication

Before a remote server allows access, the user must authenticate.

Two important SSH authentication approaches are:

- Password authentication
- SSH key authentication

---

## Password Authentication

Password authentication is familiar and simple:

```text
Username + Password
        ↓
SSH Server
        ↓
Authentication
```

However, passwords can be:

- Guessed
- Stolen
- Reused
- Obtained through credential leaks
- Targeted by automated login attempts

Internet-facing SSH servers can receive repeated automated attempts using common usernames and passwords.

This connects directly with the authentication-log investigation from **Day 59**.

---

# SSH Key Authentication

SSH keys use a **public/private key pair**.

```text
Local Machine                    Remote Server

Private Key  ---------------->  Public Key
(stays secret)                  (stored on server)
```

The important rule is:

> The private key should remain secret and should never be sent to the server.

The public key can be placed on a server.

During authentication, the SSH client uses the private key to prove possession of the corresponding key without sending the private key itself across the network.

This is an example of the broader idea of **asymmetric cryptography**.

---

# Private Key vs Public Key

| Private Key | Public Key |
|---|---|
| Must remain secret | Can be shared |
| Stored on the client | Stored on trusted servers |
| Used to prove identity | Used by the server for verification |
| Highly sensitive | Designed to be distributed |
| Must have strict permissions | Does not require the same secrecy |

A private key should never be treated like an ordinary file.

If an unauthorized person obtains a private key whose corresponding public key is trusted by a server, that person may be able to authenticate to that server.

---

# Hands-On Task

## Step 1 — Check the SSH Client

I first ran:

```bash
ssh
```

The SSH client was available in my Ubuntu environment.

This confirmed that SSH was installed and ready to use.

---

## Step 2 — Generate an Ed25519 SSH Key Pair

I generated an SSH key pair using:

```bash
ssh-keygen -t ed25519
```

I accepted the default file location and created the key without a passphrase for this learning exercise.

The key files were saved as:

```text
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

The two files represent:

```text
id_ed25519
    ↓
Private key

id_ed25519.pub
    ↓
Public key
```

---

# Step 3 — Inspect SSH Key Permissions

I checked the `.ssh` directory:

```bash
ls -l ~/.ssh
```

The important permissions were:

```text
-rw-------  ... id_ed25519
-rw-r--r--  ... id_ed25519.pub
```

The private key had:

```text
-rw-------
```

This corresponds to:

```bash
chmod 600 id_ed25519
```

Meaning:

```text
Owner:  read + write
Group:  no access
Others: no access
```

The public key had less restrictive permissions because it is designed to be shared.

---

# Step 4 — Examine the Public Key

I attempted to read the `.ssh` directory itself:

```bash
cat ~/.ssh/
```

This correctly returned an error because `.ssh` is a directory, not a regular file.

I then accessed the public key specifically:

```bash
cat ~/.ssh/id_ed25519.pub
```

The public key could be displayed safely for inspection.

I did **not** expose or publish the private key.

---

# How SSH Key Authentication Works

The basic process can be understood as:

```text
Client has private key
        ↓
Server has matching public key
        ↓
Client requests authentication
        ↓
Server verifies cryptographic proof
        ↓
Access is granted if verification succeeds
```

The private key itself does not need to travel across the network.

This is one of the most important security properties of key-based authentication.

---

# Why Private Key Permissions Matter

The private key is a sensitive authentication credential.

If another local user can read the private key, they may be able to obtain a credential that can authenticate to servers trusting the corresponding public key.

That is why SSH commonly requires restrictive permissions on private keys.

For example:

```bash
chmod 600 ~/.ssh/id_ed25519
```

This gives the owner read/write access while preventing group and other users from accessing the file.

SSH may also reject a private key if its permissions are too open.

---

# SSH as an Attack Surface

SSH provides powerful remote access, which also makes it an attractive target.

An internet-facing SSH server may receive automated attempts involving:

- Common usernames
- Password guessing
- Brute-force attempts
- Stolen credentials
- Leaked credentials
- Automated scanning

A large number of failed authentication events does not automatically mean that a targeted attacker is present.

Many internet-facing systems receive background automated scanning and login attempts.

These events can appear in authentication logs and become useful evidence during security investigations.

---

# Connection to Day 59

On **Day 59**, I investigated authentication logs and observed repeated failed login attempts.

Today's SSH lesson helped me understand one possible reason for this type of activity.

A publicly reachable SSH service can attract automated programs that repeatedly attempt authentication.

This created a stronger connection between:

```text
SSH service
     ↓
Authentication attempts
     ↓
Authentication logs
     ↓
Security investigation
```

---

# SSH Hardening

Because SSH provides powerful access, it should be properly secured.

Important SSH hardening practices include:

### Use strong authentication

Prefer strong authentication methods such as SSH keys where appropriate.

### Disable direct root login

Avoid allowing direct remote login as the root account.

This reduces the risk associated with exposing the most privileged account directly.

### Limit who can connect

Only authorized users should be allowed to access the SSH service.

### Monitor authentication logs

Failed and successful authentication events can help identify suspicious activity.

### Reduce unnecessary exposure

If SSH does not need to be accessible from the entire internet, its exposure should be reduced through appropriate network controls.

### Protect private keys

Private keys should have restrictive permissions and should never be shared publicly.

---

# Changing the SSH Port

SSH commonly uses port 22.

Changing the default SSH port can sometimes reduce automated scanning noise because many automated tools scan common ports.

However:

> Changing the port is not a substitute for real SSH security controls.

Strong authentication, access restrictions, monitoring, and appropriate network exposure are more important security measures.

---

# Related Tool: SCP

SSH is also used by related tools such as **SCP (Secure Copy Protocol)** for transferring files through an SSH connection.

SCP can be useful when working with remote systems, for example:

- Transferring investigation files
- Copying scripts
- Moving logs
- Retrieving evidence from a remote system

The encrypted SSH connection helps protect the transferred data in transit.

---

# Security Perspective

SSH demonstrates an important cybersecurity principle:

> A necessary service can also become an attack surface.

SSH is extremely useful because it provides remote access.

At the same time, that remote access means an exposed SSH service must be protected carefully.

The objective is not to remove useful services simply because they can be attacked.

The objective is to **secure the access point while keeping the service useful**.

---

# Key Takeaways

- **SSH (Secure Shell)** provides secure remote command-line access.
- SSH uses a **client-server model**.
- The SSH server commonly listens on **port 22**.
- SSH encrypts communication between the client and server.
- Password authentication is simple but can be targeted by guessing and automated attacks.
- SSH keys use a **public/private key pair**.
- The **private key must remain secret**.
- The public key can be stored on servers that should trust the corresponding private key.
- Private keys require restrictive permissions such as:
  ```bash
  chmod 600 ~/.ssh/id_ed25519
  ```
- Internet-facing SSH services can attract automated authentication attempts.
- Authentication logs can provide evidence of suspicious login activity.
- SSH hardening includes strong authentication, limiting users, disabling direct root login, monitoring logs, and reducing unnecessary exposure.
- Changing the SSH port may reduce scanning noise but is not a security control by itself.
- SSH extends Linux skills from working locally to securely working with remote systems.

---

# Connection to the Linux Journey

The Linux skills I have been learning can now be viewed as a progression:

```text
Operate Linux
      ↓
Investigate Linux
      ↓
Manage Linux
      ↓
Automate Linux
      ↓
Access Linux Remotely
```

SSH does not replace the Linux skills I already learned.

Instead, it extends where those skills can be used.

Commands for:

- Processes
- Files
- Logs
- Networking
- Permissions
- Scripts
- Scheduled tasks

can become useful on remote systems as well.

---

# Day 63 Summary

Today's lesson changed how I think about Linux access.

A Linux machine does not have to be physically in front of me for me to investigate or manage it. SSH provides a secure way to reach remote systems through the command line.

At the same time, SSH is a powerful doorway into a system, which makes protecting that doorway essential.

The most important lesson for me was:

**Powerful access requires strong protection.**

**Day 63 complete. 🔐🐧**
