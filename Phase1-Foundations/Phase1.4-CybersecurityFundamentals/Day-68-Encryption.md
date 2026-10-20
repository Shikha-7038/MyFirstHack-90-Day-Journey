# Day 68 --- Encryption

## Overview

Encryption is one of the fundamental technologies used to protect
information in modern systems. It transforms readable information into
an unreadable form so that only someone with the appropriate key can
recover the original information.

This lesson focused on what encryption does, its core vocabulary, where
it is used, the key-management problem, its limitations, and how
ransomware can misuse it.

## Core Encryption Vocabulary

### Plaintext

**Plaintext** is the original information in a readable form before
encryption.

### Ciphertext

**Ciphertext** is the scrambled, unreadable form of information produced
after encryption.

### Encryption

**Encryption** is the process of converting plaintext into ciphertext
using an encryption algorithm and a key.

``` text
Plaintext + Key
      ↓
  Encryption
      ↓
Ciphertext
```

### Decryption

**Decryption** is the process of converting ciphertext back into
plaintext using the appropriate key.

``` text
Ciphertext + Key
      ↓
  Decryption
      ↓
Plaintext
```

### Key

A **key** is secret information used by a cryptographic system to
control encryption and/or decryption.

A useful mental model is a locked box: the message is protected, the
encrypted information can travel through an untrusted environment, and
the appropriate key allows authorized access.

## Where the Security Lives

A fundamental principle of modern cryptography is:

> **Security should depend on keeping the key secret, not on keeping the
> algorithm secret.**

Modern encryption algorithms are generally designed to remain secure
even when attackers know how the algorithm works.

``` text
Algorithm = Public method
Key       = Secret information
```

## Encryption and the CIA Triad

### Confidentiality

Encryption primarily protects **Confidentiality** by preventing
unauthorized people from understanding protected information.

### Integrity

Encryption can contribute to protecting **Integrity** when combined with
appropriate cryptographic mechanisms. Encryption by itself should not be
treated as a complete integrity guarantee.

### Availability

Encryption does not inherently guarantee Availability. Ransomware
demonstrates that encryption can instead be misused to attack
availability.

## Encryption in Transit

**Encryption in transit** protects information while it is moving
between systems.

Examples include: - HTTPS - SSH - Secure messaging - Other encrypted
network connections

``` text
Your Device
     ↓
Encrypted connection
     ↓
Website / Server
```

This connects to Day 33 network eavesdropping and Day 63 SSH: protected
communication is not simply exposed as readable plaintext while
travelling across the network.

## Encryption at Rest

**Encryption at rest** protects information while it is stored.

Examples include: - Smartphone storage - Laptop storage - Files -
Databases - Backups - Storage devices

``` text
Stored information
       ↓
    Encryption
       ↓
Protected stored data
```

This matters when a device is lost or stolen. A stolen encrypted device
does not automatically give an attacker readable access to all of its
stored data.

## Encryption in Transit vs. At Rest

  -----------------------------------------------------------------------
  Type                    Protects                Examples
  ----------------------- ----------------------- -----------------------
  Encryption in transit   Data while moving       HTTPS, SSH, secure
                                                  messaging

  Encryption at rest      Data while stored       Phone storage, laptop
                                                  disk, databases,
                                                  backups
  -----------------------------------------------------------------------

A secure system may need both because information can be exposed while
moving and while stored.

## The Key Management Problem

A central practical challenge is:

> **How can authorized people securely obtain and manage the keys they
> need?**

Suppose two people want to exchange encrypted messages and both need the
same secret key. If they have never communicated securely before, simply
sending the key through an untrusted network could allow an eavesdropper
to intercept it.

``` text
Person A
   ↓
Secret key
   ↓
Untrusted network
   ↓
Person B
```

This creates the key-establishment problem:

> **How can two parties securely establish a secret when they do not
> already have a secure way to share that secret?**

The point of the lesson is to recognize why this is difficult. Day 69
introduces asymmetric encryption as a way to approach this problem.

## Key Management

Key management includes:

``` text
Generate → Distribute → Store → Protect
                         ↓
                 Rotate → Revoke → Retire
```

-   **Generate:** create strong cryptographic keys.
-   **Distribute:** make keys available to authorized users or systems
    without exposing them.
-   **Store:** keep keys in secure locations.
-   **Protect:** prevent unauthorized access or copying.
-   **Rotate:** replace keys when appropriate.
-   **Revoke:** invalidate keys that should no longer be trusted.
-   **Retire:** remove keys from active use when they are no longer
    needed.

Poor key management can undermine otherwise strong encryption.

## Why Asymmetric Encryption Matters

Symmetric encryption generally involves parties sharing a secret key.
The difficulty of securely sharing that secret leads directly to the
study of **asymmetric encryption**.

``` text
Encryption
     ↓
Key-management problem
     ↓
Secure key establishment
     ↓
Asymmetric encryption
        (Day 69)
```

This also connects to the SSH key concepts encountered earlier.

## Limits of Encryption

Encryption is powerful, but it is not a complete security solution.

### Compromised Endpoints

If an attacker compromises a computer or phone, they may be able to
access information after the system has legitimately decrypted it.

``` text
Encrypted data
      ↓
   Decryption
      ↓
Readable data
      ↓
Compromised endpoint
      ↓
Attacker may access it
```

Encryption cannot replace endpoint security.

### Leaked or Compromised Keys

If an attacker obtains the key needed to decrypt information, encryption
may no longer protect that information from the attacker.

### Vulnerable Systems

Encryption does not remove vulnerabilities from the system being
accessed. A website can use HTTPS while the application itself still
contains software vulnerabilities, authentication weaknesses,
authorization problems, or misconfigurations.

### Not Complete Security

A secure system normally needs multiple layers, including
authentication, access controls, secure configuration, patch management,
endpoint protection, monitoring, logging, network security, encryption,
and backup/recovery.

## Ransomware and the Misuse of Encryption

Encryption is normally used to protect information. Ransomware
demonstrates that the same technology can be weaponized.

### Normal protective use

``` text
Readable data
      ↓
  Encryption
      ↓
Protected data
```

### Ransomware

``` text
Readable data
      ↓
Unauthorized encryption
      ↓
Inaccessible data
```

Ransomware can encrypt files so legitimate users can no longer access
them. Attackers may then demand payment in exchange for a claimed
decryption key or recovery mechanism.

Normal encryption can protect **Confidentiality**, while ransomware can
use encryption to attack **Availability**.

The technology itself is not inherently harmful; the difference is who
controls the encryption and keys and for what purpose.

# Day 68 Task --- See the Encryption Around You

This was an observing-and-thinking exercise. No terminal commands were
required.

## Step 1 --- Define the Core Vocabulary

Write one-sentence definitions of plaintext, ciphertext, encryption,
decryption, and key, then record the central insight that security lives
in the key rather than the method.

Suggested answers:

-   **Plaintext:** The original information in a readable form before
    encryption.
-   **Ciphertext:** The scrambled, unreadable form produced by
    encryption.
-   **Encryption:** The process of converting plaintext into ciphertext
    using an algorithm and key.
-   **Decryption:** The process of converting ciphertext back into
    plaintext using the appropriate key.
-   **Key:** Secret information that controls encryption and/or
    decryption.

**Central insight:** The security of a modern encryption system depends
on protecting the key, not hiding the encryption method.

## Step 2 --- Spot Encryption in Transit

Open a browser and visit major websites. Look for the secure connection
indicator and confirm that the sites use HTTPS.

Record: - Which websites were checked - Whether they used HTTPS -
Whether any site lacked a secure connection - What this demonstrates
about encryption in transit

Example documentation format:

``` text
Sites checked:
- Google
- GitHub
- LinkedIn

Result:
The sites used HTTPS/secure connections.

Observation:
HTTPS demonstrates encryption in transit, protecting communication
between the device and the website from being exposed as readable data.
```

## Step 3 --- Find Encryption at Rest

Consider where encryption protects stored information: - Smartphone
storage - Laptop storage - Files - Databases - Backups

Consider whether a phone requires a passcode or biometric authentication
and whether laptop storage uses device/full-disk encryption where
supported.

The main reasoning point is that a stolen encrypted device is generally
a much smaller confidentiality risk than an otherwise comparable
unencrypted device because the stored data is protected by encryption
and access controls.

## Step 4 --- Reason About the Key Problem

Consider this scenario:

> You and a friend want to exchange encrypted messages, and both of you
> need the same secret key.

Ask:

> **How would you securely get the secret key to your friend without an
> eavesdropper intercepting it?**

The point is not to solve the problem completely. The goal is to
understand why it is difficult and recognize that it leads into
asymmetric encryption in Day 69.

## Step 5 --- Reason About the Limits

Identify at least two things encryption does not protect against.

Examples:

-   **Compromised endpoint:** An attacker who controls the endpoint may
    access information after it has been decrypted.
-   **Leaked or compromised key:** If an attacker obtains the necessary
    key, encryption may no longer protect the information from that
    attacker.
-   **Not complete security:** Encryption does not remove application
    vulnerabilities, authentication weaknesses, or other security
    problems.

Explain ransomware:

> Ransomware weaponizes encryption by encrypting a victim's files
> without authorization, making them inaccessible to legitimate users
> and potentially demanding payment for decryption.

## What to Capture

-   One-sentence definitions of the five core vocabulary terms
-   The insight that security lives in the key rather than the method
-   Websites checked for HTTPS
-   Observations about encryption in transit
-   Where data is protected at rest
-   Why encryption matters if a device is stolen
-   Reasoning about the secret-key sharing problem
-   Two or more limitations of encryption
-   How ransomware weaponizes encryption

# Connections to the MyFirstHack Journey

### Day 33 --- Network Investigation

Encryption connects to network eavesdropping. Encrypted traffic prevents
an observer from simply reading protected communication as plaintext.

### Day 63 --- SSH

SSH provided an earlier practical example of secure communication. Day
68 explains the encryption concept behind that kind of protection at a
deeper level.

### Day 66 --- CIA Triad

Encryption primarily supports **Confidentiality**, while ransomware
demonstrates how encryption can also be abused to affect
**Availability**.

### Day 67 --- Threat, Vulnerability, and Risk

Encryption is one security control that can reduce particular risks, but
it does not eliminate every threat or vulnerability.

### Day 69 --- Symmetric vs. Asymmetric Encryption

The next lesson explores different encryption approaches and how
asymmetric cryptography helps address the key-sharing problem.

### Day 70 --- Hashing

Hashing is a different cryptographic technique. Unlike encryption,
hashing is designed as a one-way transformation and has important uses
in integrity and other security applications.

# Day 68 Concept Map

``` text
                    ENCRYPTION
                         │
          ┌──────────────┼──────────────┐
          │              │              │
     Core concepts   Where used     Key management
          │              │              │
 Plaintext           In transit      Generate
 Ciphertext          At rest         Distribute
 Encryption                           Store
 Decryption                           Protect
 Key                                  Rotate
                                      Revoke
                                      Retire
          │
          ▼
   Security depends
      on the key
          │
          ▼
    Key-sharing problem
          │
          ▼
 Asymmetric encryption
      (Day 69)
```

# Key Takeaways

-   Encryption transforms plaintext into ciphertext so protected
    information cannot simply be read by unauthorized parties.
-   Decryption converts ciphertext back into plaintext using the
    appropriate key.
-   The key is the critical secret; the algorithm does not need to be
    secret.
-   Encryption primarily protects Confidentiality.
-   Encryption in transit protects data while it moves across networks.
-   Encryption at rest protects stored data.
-   Key management is a major practical security challenge.
-   Encryption does not protect against every threat, including
    compromised endpoints and leaked keys.
-   Encryption is not a complete security solution by itself.
-   Ransomware can misuse encryption to make data inaccessible and
    attack Availability.
-   The key-sharing problem leads naturally into asymmetric encryption,
    the focus of Day 69.

# Overall Security Model

``` text
Readable information
        ↓
   Encryption + Key
        ↓
     Ciphertext
        ↓
   Untrusted environment
        ↓
 Decryption + Appropriate Key
        ↓
Readable information
```

Effective protection also depends on:

``` text
Strong cryptographic method
          +
Secure key management
          +
Correct implementation
          +
Secure endpoints
          +
Other security controls
          ↓
Effective security
```

Encryption is therefore a foundational security technology with a
specific purpose, specific strengths, and specific limits.
