# Day 70 — Hashing

## What is Hashing?

Hashing is the process of taking any input and passing it through a **hash function** to produce a fixed-length value called a **hash** or **digest**.

The input can be text, files, passwords, images, databases, or other digital data.

### Simple definition

> Hashing creates a fixed-length digital fingerprint of data that can be used to verify or compare the data without recovering the original through the hash function.

Hashing is different from encryption. Encryption is designed to hide information while allowing authorized users to recover the original information. Hashing is designed mainly for verification and comparison.

---

## How Hashing Works

```text
Input → Hash Function → Hash
```

For example:

```text
"Hello World"
      ↓
 Hash Function
      ↓
Fixed-length Hash
```

A particular algorithm determines the output size. For example, SHA-256 always produces a **256-bit hash**, regardless of whether the input is a short word or a very large file.

---

# Core Properties of a Cryptographic Hash

## Deterministic

A hash function is deterministic, meaning:

> The same input always produces the same hash.

```text
Hello World → Hash A
Hello World → Hash A
```

This makes hashing useful for comparison and verification.

## Fixed-Length Output

A particular hash algorithm produces an output of a fixed size.

For example, SHA-256 always produces **256 bits = 32 bytes = 64 hexadecimal characters**.

```text
Small input → SHA-256 → 64 hexadecimal characters
Large file → SHA-256 → 64 hexadecimal characters
```

## One-Way

Calculating `Input → Hash` is easy and practical, but `Hash → Original input` is not feasibly reversible through the hash function.

This is useful for password protection. However, one-way does not mean weak passwords can never be discovered. Attackers can guess possible passwords, process those guesses, and compare the results.

## Collision Resistance

A collision occurs when two different inputs produce the same hash. Because there are infinitely many possible inputs but a fixed number of hash outputs, collisions must theoretically exist.

A cryptographic hash is designed so that it is **computationally infeasible to deliberately find two different inputs with the same hash**.

## Avalanche Effect

The avalanche effect means that a very small change in the input can cause a dramatically different hash.

```text
Hello World → Hash A
Hello world → Hash B
```

Only one character changed, but the resulting hashes can look completely unrelated.

If the original input is restored, the original hash appears again because hashing is deterministic.

## One Example Demonstrating Multiple Properties

```text
Hello World → Hash A
Hello world → Hash B
Hello World → Hash A
```

This demonstrates:

- **Avalanche effect:** one small change produces a very different hash.
- **Deterministic:** restoring the exact original input produces the original hash again.
- **Fixed-length:** each SHA-256 output remains the same length.
- **One-way:** the hash is not normally used to recover the original text.

---

# Hashing for Integrity Verification

One major use of hashing is checking whether data has changed.

```text
Original file
     ↓
Calculate hash
     ↓
Expected hash
```

Later:

```text
Downloaded file
     ↓
Calculate hash
     ↓
Compare with expected hash
```

### If the hashes match

The downloaded file's contents match the contents represented by the expected hash.

### If the hashes do not match

Something is different. Possible reasons include corruption, modification, tampering, a different version, or an incomplete download.

The avalanche effect makes hashing sensitive to even small changes.

### Important limitation

A matching hash does not automatically prove that a file came from a trustworthy source. If an attacker can replace both the file and expected hash, simple comparison may not detect the attack. Digital signatures or authenticated/trusted distribution channels can provide stronger authenticity.

---

# Hashing for Password Protection

A properly designed system should **not store users' passwords in plaintext**.

Instead, it stores a protected password representation produced using a password-hashing/key-derivation mechanism.

Simplified flow:

```text
User creates password
        ↓
Password hashing
        ↓
Stored password representation
```

When the user logs in:

```text
Password entered
        ↓
Password hashing/verification
        ↓
Compare with stored value
        ↓
Match → Login allowed
```

The system can verify whether the entered password is correct without needing to store the original password itself.

## Why Plaintext Passwords Are Dangerous

If a database stores an actual password, a database breach exposes that password directly.

With properly protected password storage, the database contains a protected representation instead of the plaintext password.

Therefore:

> "Passwords were hashed" is very different from "passwords were stored in plaintext."

However, hashed passwords are not automatically safe.

## How Attackers Can Guess Weak Passwords

An attacker who obtains password representations can try possible passwords:

```text
"password123"
      ↓
Password-processing function
      ↓
Compare with stolen value
```

They can repeat this with many guesses. Weak and common passwords are therefore easier to attack.

Password security also depends on strong passwords, unique salts, deliberately slow password-hashing algorithms, and appropriate storage practices.

## Salting

A **salt** is a unique random value associated with a password before password hashing. Its purpose is to ensure that identical passwords do not produce identical stored password values.

```text
Password + unique salt → Stored value A
Same password + different salt → Stored value B
```

Salts also make precomputed lookup attacks less useful.

## Slow Password Hashing

General-purpose cryptographic hashes are designed to be fast. That is useful for file integrity, but it also allows attackers to make many guesses quickly.

Password-specific algorithms deliberately make each password guess more expensive.

Common password-hashing approaches include **Argon2id, bcrypt, and scrypt**.

---

# Hashing vs Encryption

| Encryption | Hashing |
|---|---|
| Designed to be reversible | Designed to be one-way |
| Uses an encryption key | Plain cryptographic hashing uses no encryption key |
| Original data can be recovered with the correct key | Original input is not normally recovered from the hash |
| Primarily used for confidentiality | Used for integrity and password protection |
| Protects information from unauthorized reading | Helps verify or compare information |

### Simple mental model

**Encryption:** Hide it → recover it later.

**Hashing:** Fingerprint it → verify or compare it later.

---

# Hashing and the CIA Triad

### Confidentiality

**Encryption** is a major tool for protecting confidentiality.

> Who can see the information?

### Integrity

**Hashing** can help verify integrity.

> Has the information changed?

### Availability

Hashing does not directly provide availability. Availability is supported through mechanisms such as backups, redundancy, reliable infrastructure, disaster recovery, and denial-of-service protection.

---

# Hashing in Real-World Security

- **Software integrity:** published checksums can be compared with downloaded files.
- **File integrity monitoring:** important files can be hashed and later compared to detect changes.
- **Digital forensics:** investigators can hash evidence files to help demonstrate that they have not changed since collection.
- **Password protection:** password-specific hashing mechanisms protect stored password representations.
- **Digital signatures:** cryptographic hashes are commonly used as part of digital-signature processes.

---

# Important Limitations

### Hashing does not provide secrecy

If information needs to be hidden and later recovered, encryption is the appropriate tool.

### Hashing does not automatically authenticate data

A plain hash can show whether data matches an expected value, but stronger integrity and authenticity may require a **MAC or digital signature**.

### Hashing does not make weak passwords safe

Attackers can guess common passwords and compare their processed values with stolen password representations.

### Hashing does not remember history

A hash represents the data in its current state.

```text
Original file → Hash A
Change one character → Hash B
Change it back → Hash A
```

The hash function does not remember that the file was temporarily changed. The final hash depends on the final contents.

---

# Day 70 Tasks

## Task — Tell Encryption and Hashing Apart

### Step — Define a hash

A hash function takes any input, such as a password or file, and converts it into a fixed-length digital fingerprint that can be used to identify or verify that input without storing the original data.

The core properties are deterministic, fixed-length, one-way, collision-resistant, and avalanche effect.

### Step — Explain encryption vs hashing

**Encryption** is used when information needs to remain secret but must be recoverable later using the correct key.

**Hashing** creates a digital fingerprint mainly used for verification and comparison.

```text
Encryption:
Two-way / reversible
Uses a key
Primarily protects confidentiality

Hashing:
One-way
No encryption key for a plain cryptographic hash
Helps with integrity and password protection
```

### Step — Explain file integrity verification

If a website provides a SHA-256 hash for a downloadable file, I can calculate the SHA-256 hash of my downloaded copy and compare the two values.

If the hashes match, the contents of my file match the expected file represented by the trusted published hash.

If the hashes do not match, something is different. The file may have been corrupted, modified, tampered with, or may simply be a different version.

The avalanche effect makes even a small change likely to produce a very different hash.

A matching hash should be interpreted in relation to a trusted expected hash; hashing alone does not prove who created the file.

### Step — Explain password protection

A properly designed service should not store my actual password in plaintext.

Instead, it uses a password-specific hashing/key-derivation mechanism and stores the resulting protected representation.

When I log in, the password I enter is processed again and compared with the stored value.

If a database is breached, attackers receive the stored password representations rather than plaintext passwords.

However, attackers can still guess weak passwords and compare the processed guesses with stolen values.

That is why password security also uses strong passwords, unique salts, and deliberately slow password-hashing algorithms such as Argon2id, bcrypt, or scrypt.

### Step — Identify hashing in everyday security

Two common examples are:

**Online accounts:** Password-protection systems use password hashing/key-derivation mechanisms so the service does not need to store plaintext passwords.

**Software downloads:** A publisher may provide a checksum such as SHA-256 so users can verify that a downloaded file matches the expected contents.

After a breach, hearing that passwords were properly hashed is more reassuring than hearing that passwords were stored in plaintext, but hashing does not eliminate all password-related risk.

---

# Key Takeaways

- **Hashing** converts input data into a fixed-length digital fingerprint.
- A cryptographic hash is **deterministic**: the same input produces the same hash.
- Hash outputs are **fixed-length** for a given algorithm.
- Hashing is designed to be **one-way** and not feasibly reversible through the hash function.
- **Collision resistance** makes it computationally difficult to deliberately find different inputs with the same hash.
- The **avalanche effect** means a tiny input change can produce a dramatically different hash.
- Hashing is useful for **integrity verification**.
- Hashes can be used to compare a downloaded file against a trusted expected hash.
- Passwords should **not be stored in plaintext**.
- Password protection uses password-specific hashing/key-derivation mechanisms with **unique salts** and appropriate work factors.
- Weak passwords can still be attacked through guessing, even when stored using hashes.
- **Encryption and hashing have different purposes:** encryption hides and later recovers; hashing fingerprints and verifies.
- Hashing helps with **integrity**, while encryption primarily helps with **confidentiality**.
- Hashing does not remember previous versions of data; it only depends on the data's current contents.
- A plain hash does not automatically provide authenticity; stronger mechanisms such as **MACs and digital signatures** may be required.

---

# Final Mental Model

```text
                 HASHING

Any Input
    ↓
Hash Function
    ↓
Fixed-Length Digital Fingerprint
    ↓
Compare / Verify
```

```text
Core Properties

Deterministic
Fixed-Length
One-Way
Collision-Resistant
Avalanche Effect
```

```text
Main Uses

Integrity Verification
Password Protection
File Integrity Monitoring
Digital Forensics
Digital Signatures
```

### One-line memory aid

> **Encryption hides information. Hashing fingerprints information.**

---

# Connection to Previous Learning

**Day 68 — Encryption:** Encryption protects information by making it unreadable to unauthorized parties while allowing authorized recovery.

**Day 69 — Symmetric & Asymmetric Cryptography:** Symmetric cryptography provides efficient encryption for bulk data, while asymmetric/public-key cryptography helps with authentication, key establishment, and digital signatures.

**Day 70 — Hashing:** Hashing creates a one-way digital fingerprint that can be used for verification and password protection.

### Simple overall picture

**Encryption → Hide information**

**Symmetric + Asymmetric → Build secure communication**

**Hashing → Fingerprint and verify information**
