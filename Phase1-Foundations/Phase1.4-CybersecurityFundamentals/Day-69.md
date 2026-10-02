# Day 69 --- Symmetric vs Asymmetric Encryption

## Topic

**Symmetric vs Asymmetric Encryption**

Day 69 focuses on why symmetric and asymmetric cryptography exist, the
key-sharing problem, how both approaches work together in secure
communication, and how these concepts connect to SSH and HTTPS.

## 1. The Key-Sharing Problem

Symmetric encryption uses the same secret key for both encryption and
decryption. This creates an important problem: **How can two people who
have never communicated securely share the same secret key when an
attacker may be watching the network?**

If the secret key is sent over an untrusted network, an eavesdropper
could potentially capture it. This is known as the **key-distribution or
key-sharing problem**.

Asymmetric cryptography addresses this problem by using two related keys
instead of one shared secret.

## 2. Symmetric Encryption

**Symmetric encryption** uses a single shared secret key for both
encryption and decryption.

``` text
Plaintext → Encryption + shared key → Ciphertext
Ciphertext → Decryption + same shared key → Plaintext
```

### Main characteristics

-   One shared secret key.
-   The same key is used for encryption and decryption.
-   Very fast and computationally efficient.
-   Well suited for large amounts of data.
-   Commonly used for ongoing communication and bulk data encryption.
-   Main challenge: securely sharing the key before communication
    begins.

## 3. Asymmetric Cryptography

**Asymmetric cryptography**, also called **public-key cryptography**,
uses a mathematically related pair of keys: a **public key** and a
**private key**.

-   The **public key** can be shared openly.
-   The **private key** must remain secret.
-   Public-key cryptography helps with authentication and secure
    session/key establishment.
-   It is more computationally expensive than symmetric encryption.

In public-key encryption, information encrypted to a recipient's public
key can be decrypted using the corresponding private key. Public-key
cryptography is also used for authentication and digital signatures, so
it is broader than encryption alone.

## 4. Why the Public Key Can Be Public

The security of public-key cryptography does not depend on hiding the
public key. An attacker may see it, but the important secret is the
**private key**.

The private key stays with its owner and does not need to travel across
the network. This is what makes public-key cryptography useful when two
parties do not already share a secret.

``` text
Public Key  → can be shared openly
Private Key → stays with its owner
```

## 5. Symmetric vs Asymmetric Cryptography

  -----------------------------------------------------------------------
  Feature                 Symmetric Encryption    Asymmetric Cryptography
  ----------------------- ----------------------- -----------------------
  Keys                    One shared secret key   Public + private key
                                                  pair

  Speed                   Very fast               Slower

  Computational cost      Lower                   Higher

  Main strength           Efficient data          Authentication and
                          encryption              secure key
                                                  establishment

  Main challenge          Securely sharing the    Greater computational
                          key                     cost

  Best suited for         Bulk data               Secure setup,
                                                  authentication, key
                                                  establishment
  -----------------------------------------------------------------------

## 6. Why Both Types Exist

Symmetric encryption is fast and efficient but has the key-sharing
problem. Asymmetric cryptography helps with authentication and
establishing shared secrets without directly distributing a private
secret, but it is slower and more computationally expensive.

Therefore, secure systems commonly combine them rather than choosing one
over the other.

> **Asymmetric/public-key cryptography → authentication and secure
> session/key establishment**\
> **Symmetric encryption → fast encryption of the actual session data**

## 7. How They Work Together

A simplified architecture is:

``` text
Asymmetric / Public-Key Cryptography
              ↓
Authentication + Secure Session Establishment
              ↓
       Symmetric Session Keys
              ↓
        Symmetric Encryption
              ↓
        Actual Session Data
```

The public-key part handles the difficult setup, while the symmetric
part handles the large amount of data efficiently.

> **Asymmetric = secure setup**\
> **Symmetric = fast data protection**

## 8. Establishing a Secure Connection

Consider a browser connecting to a secure website. The browser and
website may have never communicated before, so they cannot simply assume
that they already share a secret key.

### Step 1 --- Browser connects to the website

The browser starts communicating with the server and needs to establish
a secure communication context.

### Step 2 --- Public-key cryptography is involved

The server has public-key credentials, typically represented through a
certificate and its associated public key. Public-key cryptography helps
with authentication and secure session establishment. The server's
private key remains secret.

### Step 3 --- Session secrets are established

The browser and server establish the secret material needed to protect
their communication. Modern protocols can use key-agreement mechanisms,
such as Diffie--Hellman variants, rather than simply sending a symmetric
key encrypted with a public key.

The important concept is that the two sides can establish shared session
secrets without sending the server's private key across the network.

### Step 4 --- Symmetric encryption protects the data

Once the session is established, symmetric cryptography is used because
it is much faster, allowing the actual communication to be protected
efficiently.

``` text
Browser + Website
       ↓
Public-key cryptography
       ↓
Authentication / secure session establishment
       ↓
Symmetric session keys
       ↓
Symmetric encryption
       ↓
Encrypted web communication
```

## 9. The Key-Sharing Problem and Its Solution

Two strangers want to communicate securely, but there is no pre-shared
secret.

If one person simply sends a symmetric key across the network, an
attacker could potentially capture it.

Public-key cryptography allows information needed for secure
communication to be exchanged without requiring the private key to
travel.

``` text
Public key → can be shared
Private key → stays secret
```

This makes it possible to establish secure communication between parties
that did not previously share a secret.

## 10. HTTPS and the Browser Padlock

HTTPS is a practical example of public-key cryptography and symmetric
cryptography working together.

When a browser connects to a website securely, public-key cryptography
helps with authentication and secure session establishment. After
session secrets are established, symmetric encryption efficiently
protects the actual communication.

``` text
Browser + Website
       ↓
Public-key cryptography
       ↓
Authentication / secure session establishment
       ↓
Symmetric session keys
       ↓
Symmetric encryption
       ↓
Encrypted web communication
```

The browser padlock therefore represents more than simply "encryption";
it represents a secure communication process involving authentication,
key establishment, and efficient encrypted communication.

## 11. SSH and Public-Key Cryptography

An SSH key pair consists of a public key and a private key.

``` text
Public Key
    ↓
Can be placed on the server

Private Key
    ↓
Stays on the local machine
```

The public key can safely be placed on the server because it is designed
to be shared. The private key does not need to be sent to the server.

SSH can use public-key cryptography to authenticate the client by
demonstrating possession of the corresponding private key without
transmitting the private key itself.

### Important distinction

SSH should not be described as using asymmetric encryption for all
communication. Public-key cryptography is used for functions such as
authentication and key establishment, while symmetric encryption
protects the ongoing session data efficiently.

## 12. Public-Key Cryptography Has More Than One Use

Public-key cryptography can support several security functions:

### Encryption

A public key can be used to encrypt information intended for the owner
of the corresponding private key.

### Authentication

Public-key cryptography can help prove that a party possesses the
corresponding private key.

### Digital signatures

A private key can be used to create a digital signature, while the
corresponding public key can be used to verify it.

Therefore, public-key cryptography is broader than simply "encrypt with
the public key and decrypt with the private key."

## 13. Why Asymmetric Cryptography Is Not Used for Everything

Asymmetric cryptography is computationally more expensive, while
symmetric encryption is much faster.

For a secure connection that transfers a large amount of information,
symmetric encryption is therefore used for the actual data.

``` text
Public-Key Cryptography
        ↓
Secure setup
Authentication
Key establishment
        ↓
Symmetric Cryptography
        ↓
Bulk data encryption
```

## 14. Communication With Strangers

Public-key cryptography means secure communication does not require
every pair of communicating parties to have already exchanged a secret
key.

This is essential for the open internet. A user can securely connect to
a bank's website, an online shopping service, a remote server, a
messaging service, or a website they have never visited before without
manually exchanging a symmetric secret first.

Public-key cryptography provides mechanisms that help establish
authentication and secure session secrets over an untrusted network.

## 15. Complete Encryption Architecture

### Day 68 --- Basic encryption

``` text
Plaintext
    ↓
Encryption + Key
    ↓
Ciphertext
    ↓
Decryption + Key
    ↓
Plaintext
```

### Day 69 --- Two major approaches

``` text
Symmetric
One shared secret
        ↓
Fast bulk encryption

Asymmetric / Public-Key
Public + Private key pair
        ↓
Authentication
Secure session/key establishment
```

### Real-world combination

``` text
        Public-Key Cryptography
                  ↓
     Authentication / Key Establishment
                  ↓
          Session Secrets
                  ↓
        Symmetric Encryption
                  ↓
        Actual Session Data
```

## 16. Relationship With the CIA Triad

Encryption is particularly important for **Confidentiality**. It helps
prevent unauthorized people from understanding protected information
even if they can observe or obtain encrypted data.

Encryption alone does not provide complete security. Authentication,
integrity mechanisms, access controls, secure endpoints, and other
controls are also needed.

This connects Day 69 back to the **CIA Triad** studied on Day 66.

## 17. Important Limitations

### Compromised endpoint

If an attacker compromises a device after data has been decrypted,
encryption cannot necessarily protect the data from that attacker.

### Stolen private key

If a private key is stolen or compromised, the security provided by that
key can be undermined.

### Poor key management

Keys need to be generated, stored, protected, rotated, revoked when
compromised, and retired securely.

### Incorrect implementation

Strong cryptographic algorithms can still be used incorrectly. Security
depends not only on the algorithm but also on how cryptography is
implemented and managed.

## 18. Connection to Previous Learning

### Day 63 --- SSH

The public/private key pair used for SSH is an example of public-key
cryptography being used for authentication.

### Day 66 --- CIA Triad

Encryption primarily supports **confidentiality**, while other
cryptographic mechanisms can support integrity and authentication.

### Day 68 --- Encryption

Encryption transforms readable plaintext into ciphertext using a key and
allows protected information to be recovered through the appropriate
decryption process.

### Day 69 --- Symmetric vs Asymmetric Cryptography

Day 69 explains why there are different types of encryption and why
secure systems commonly combine them:

**Public-key cryptography → secure setup and authentication**\
**Symmetric encryption → efficient protection of session data**

------------------------------------------------------------------------

# Day 69 Task --- Trace How Strangers Establish Trust

## Step 1: Define the two kinds in your own words

### Symmetric encryption

Symmetric encryption uses one shared secret key to encrypt and decrypt
data, making it fast and suitable for protecting large amounts of
information.

### Asymmetric encryption

Asymmetric cryptography uses a mathematically related public key and
private key, allowing public-key cryptography to support secure
communication without sharing the private key.

### Single key difference

Symmetric encryption uses **one shared secret key**, while asymmetric
cryptography uses a **public/private key pair with different roles**.

## Step 2: Solve Yesterday's Problem

The key-sharing problem is:

> How can two strangers establish a secret when an attacker might be
> watching their communication?

With asymmetric cryptography, the **public key can be shared openly**
because it is designed to be public. An eavesdropper can see the public
key, but knowing the public key does not give them the corresponding
private key.

The most important secret is the **private key**, which stays with its
owner and does not need to travel across the network.

This matters because an attacker watching the communication does not
automatically obtain the private secret needed for operations that
depend on it.

## Step 3: Explain Why Both Exist

Asymmetric cryptography helps solve the **key-establishment and
authentication problem**, but it is computationally more expensive and
much slower than symmetric encryption.

Symmetric encryption is extremely fast, so it is much better for
encrypting the large amount of data exchanged during a session.

Therefore, secure systems generally combine them:

> **Asymmetric/public-key cryptography → authentication and secure
> session/key establishment**\
> **Symmetric encryption → fast encryption of the actual session data**

## Step 4: Re-explain the SSH Keys

The SSH key pair consists of:

-   **Public key** --- can be placed on the server.
-   **Private key** --- stays secret on the local machine.

It is safe to put the public key on the server because the public key is
specifically designed to be shared. The important secret is the private
key.

The private key does not need to travel to the server because SSH can
use public-key cryptography to authenticate possession of the private
key without sending the private key itself.

This is a practical example of the asymmetric/public-key idea.

> **Public key can travel. Private key stays secret.**

### Technical distinction

The SSH key pair is an example of **public-key cryptography used for
authentication**. SSH does not use asymmetric encryption for all of its
ongoing session traffic; symmetric encryption is used to efficiently
protect the established session.

## Step 5: Explain the Padlock to a Beginner

When a browser connects to a website, public-key cryptography helps the
browser and server authenticate the server and establish the secrets
needed for the session, even though they have not previously shared a
secret.

Once the session is established, symmetric encryption uses those session
secrets to protect the actual data because it is much faster.

### Simple version

> **Asymmetric handles the secure setup; symmetric handles the data.**

------------------------------------------------------------------------

# Day 69 Key Takeaways

-   **Symmetric encryption** uses one shared secret key for encryption
    and decryption.
-   Symmetric encryption is **fast and efficient**, making it suitable
    for bulk data.
-   The major challenge with symmetric encryption is **securely sharing
    the key**.
-   **Asymmetric/public-key cryptography** uses a public key and a
    private key with different roles.
-   The **public key can be shared openly**.
-   The **private key must remain secret** and does not need to travel
    across the network.
-   Public-key cryptography helps with **authentication and secure
    session/key establishment**.
-   Asymmetric cryptography is generally **slower and more
    computationally expensive** than symmetric encryption.
-   Secure systems commonly use **both types together**.
-   A simplified architecture is: **Public-key cryptography → secure
    setup → symmetric session keys → symmetric encryption of actual
    data.**
-   HTTPS uses public-key cryptography for parts of
    authentication/session establishment and symmetric cryptography for
    efficient protection of session data.
-   SSH uses public-key cryptography for functions such as
    authentication, while symmetric encryption protects the ongoing
    session.
-   Public-key cryptography is broader than encryption; it can also
    support **authentication and digital signatures**.
-   Encryption is primarily associated with **confidentiality** in the
    CIA Triad.
-   Strong cryptography still depends on **secure key management and
    correct implementation**.

## Central Mental Model

> **Asymmetric = secure setup**\
> **Symmetric = fast data protection**
