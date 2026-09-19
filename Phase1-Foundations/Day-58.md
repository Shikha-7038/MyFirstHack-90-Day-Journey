# 🐧 Day 58 — Linux Network Investigation

## 📅 Overview

**Day:** 58 of 90  
**Phase:** Linux  
**Topic:** Interrogate the Network from the Terminal  
**Environment:** Linux / WSL  
**Focus:** Network state, listening ports, process ownership, reachability, and DNS investigation

---

## 🎯 Objective

Today I investigated network activity directly from inside a Linux machine.

The goal was to understand:

- 🔌 What network services are listening
- 🔗 Which process is responsible for a listening port
- 📡 Whether a destination is reachable
- 🌐 What a domain resolves to through DNS
- 🕵️ How processes and network connections can be investigated together

This connected my previous **Networks phase** with the Linux investigation skills I have been developing.

---

# 🧠 1. Connecting Previous Learning

Yesterday, I learned about **Linux processes**.

The main question was:

> **What is running?**

Today, I added another question:

> **What is it talking to?**

This connects several concepts I learned earlier:

- 🌐 Ports
- 🔎 DNS
- 🔗 Network connections
- 📡 Beaconing
- 🛡️ Suspicious network activity

The Linux terminal now allows me to investigate these concepts directly from the machine.

---

# 🔌 2. Viewing Network State with `ss`

The first command I used was:

```bash
ss -tuln
```

### Meaning of the options

| Option | Meaning |
|---|---|
| `-t` | Show TCP sockets |
| `-u` | Show UDP sockets |
| `-l` | Show listening sockets |
| `-n` | Show numerical addresses and ports |

The command showed the network sockets currently present in the Linux environment.

### 🔊 LISTEN State

A TCP socket in the `LISTEN` state means that a service is waiting for incoming connections.

I observed DNS-related activity on **port 53**.

Port 53 is commonly associated with DNS.

### Important security lesson

A listening port is **not automatically suspicious**.

The correct approach is to ask:

> What process owns this port, and should that process be listening?

---

# 🕰️ 3. `netstat` — Older Alternative

I also used:

```bash
netstat -tuln
```

`netstat` displayed network information similar to `ss`.

### `ss` vs `netstat`

| `ss` | `netstat` |
|---|---|
| Modern Linux tool | Older tool |
| Commonly preferred today | Still appears in tutorials and documentation |
| Displays socket information | Displays similar network information |

The important part is understanding the network state rather than memorizing a specific command.

---

# 🔗 4. Connecting a Port to a Process

The next step connected today's lesson with Day 57.

I used:

```bash
sudo ss -tulpn
```

The `-p` option displays process information associated with sockets.

This creates an important investigative relationship:

```text
🔌 Port → 🧩 Process
```

During the investigation, the DNS-related listening port was associated with the Linux process:

```text
systemd-resolve
```

This demonstrated that a network service can be traced back to the process responsible for it.

### Why this matters

If an unexpected port is found, an investigator can ask:

- Which process owns it?
- Is the process legitimate?
- Why is it listening?
- Does it need network access?
- Is the service expected on this machine?

This is one of the most important connections between **process investigation and network investigation**.

---

# 📡 5. Testing Reachability with `ping`

I used:

```bash
ping -c 4 example.com
```

The `-c 4` option sends four test packets and then stops.

### `ping` helps answer:

> **Can I reach this destination, and how quickly does it respond?**

The output provides information such as:

- 📦 Packets transmitted
- 📥 Packets received
- 📉 Packet loss
- ⏱️ Round-trip response time

My test successfully received replies with **0% packet loss**.

### ⚠️ Important security point

A successful ping does **not** mean that a destination is safe.

Likewise, no ping response does not necessarily mean that the destination is down.

Some systems are configured to ignore ICMP/ping requests.

---

# 🌐 6. DNS Investigation with `dig`

Next, I used:

```bash
dig example.com
```

This allowed me to perform a DNS lookup directly from the terminal.

I also tested another domain.

### Important sections of `dig`

#### ❓ QUESTION SECTION

Shows what was requested.

For example:

```text
example.com.    IN    A
```

`A` represents an IPv4 address record.

#### ✅ ANSWER SECTION

Shows the DNS answer returned for the query.

This can contain one or more IP addresses.

#### 🖥️ SERVER

Shows which DNS server responded to the query.

#### ⏱️ Query Time

Shows how long the DNS query took.

---

# 🔎 7. Connecting `dig` to Earlier DNS Learning

On **Day 24**, I learned DNS as a concept:

```text
Domain Name
     ↓
DNS Lookup
     ↓
IP Address
```

Today, `dig` allowed me to perform that lookup myself.

This also connects to **Day 33 — DNS Spoofing**.

If DNS information is manipulated, a domain could potentially be directed to an unintended address.

Using `dig` gives an investigator a way to inspect what DNS is actually returning.

---

# 🕵️ 8. Spotting a Process “Phoning Home”

One of the main ideas from today's lesson was investigating a process that may be communicating externally.

A compromised process could potentially:

- 📤 Send stolen information
- 📥 Receive commands
- 📦 Download additional content
- 🔄 Periodically contact an external server

Repeated communication at regular intervals can resemble the **beaconing pattern** I learned about during the Networks phase.

### Investigation idea

```text
🔗 Find a connection
        ↓
🧩 Identify the process
        ↓
🌐 Identify the destination
        ↓
🔎 Investigate DNS information
        ↓
📡 Test reachability
        ↓
📝 Look for supporting evidence
```

An unfamiliar connection is a **clue**, not automatic proof of compromise.

Multiple pieces of evidence should be considered together.

---

# 🚩 9. Network Indicators Worth Investigating

Some observations can become investigation leads.

### 🔸 Unexpected external connection

A process communicating with an unfamiliar external address may require investigation.

### 🔸 Unexpected listening port

A port that no legitimate service should have open could indicate:

- Unwanted service
- Misconfiguration
- Potential backdoor

### 🔸 Repeated connections

Regular connections to the same destination may resemble beaconing.

### 🔸 Suspicious process with network activity

A process that already appears suspicious and is also communicating externally deserves closer investigation.

None of these observations alone proves that a machine is compromised.

---

# 🧩 10. Three Views of One Activity

Day 57, Day 58, and Day 59 form a useful investigation model.

| Day | View | Question |
|---|---|---|
| 🧩 Day 57 | Processes | What's running? |
| 🌐 Day 58 | Network | What is it talking to? |
| 📜 Day 59 | Logs | What happened over time? |

These are different views of the same system activity.

For example:

```text
🧩 Process
    ↓
🔗 Network Connection
    ↓
🌐 External Destination
    ↓
🔎 DNS Information
    ↓
📜 Logs
```

A good investigation moves between these views instead of relying on a single observation.

---

# 🛡️ 11. Connection to SIEM

This also connects to the **SIEM** concept learned earlier.

A SIEM collects and correlates events from different sources.

During a manual Linux investigation, I am developing a similar mindset:

```text
Process Evidence
       +
Network Evidence
       +
Log Evidence
       ↓
Investigation Story
```

Instead of examining isolated events, I can connect related evidence to understand what happened.

---

# 🧰 12. Tools Learned Today

| Tool | Purpose |
|---|---|
| `ss` | View network sockets and connections |
| `netstat` | Older tool for network information |
| `sudo ss -tulpn` | Connect ports with responsible processes |
| `ping` | Test reachability and response time |
| `dig` | Perform DNS lookups |

---

# 🔐 13. Why Terminal-Based Network Investigation Matters

Wireshark is useful for examining network traffic.

However, Linux terminal tools provide a direct view from **inside the machine**.

Using the terminal, I can investigate:

- 🔌 Listening ports
- 🔗 Network connections
- 🧩 Processes associated with sockets
- 🌐 DNS responses
- 📡 Basic network reachability

This is valuable because an investigator may not always have access to:

- Network equipment
- Packet captures
- Wireshark
- Centralized monitoring tools

The machine itself can still provide useful evidence.

---

# 🧪 14. Hands-On Task Summary

### Step 1 — Network State

```bash
ss -tuln
```

Observed listening sockets and DNS-related activity.

### Step 2 — Port → Process

```bash
sudo ss -tulpn
```

Connected a listening port to the process responsible for it.

### Step 3 — Reachability

```bash
ping -c 4 example.com
```

Confirmed that the destination responded successfully and observed packet loss and response-time information.

### Step 4 — DNS Lookup

```bash
dig example.com
```

Inspected the DNS response and identified the returned address information in the **ANSWER SECTION**.

### Step 5 — Investigation Reasoning

Considered:

- 🚩 Why an unexpected listening port can be concerning
- 🔎 How to investigate an unexplained external connection
- 🖥️ Why terminal-based network visibility is useful alongside Wireshark

---

# 💡 15. Key Takeaways

- 🐧 Linux provides tools for investigating network activity directly from the terminal.
- 🔌 `ss` shows network sockets and listening ports.
- 🕰️ `netstat` is an older alternative.
- 🔗 `sudo ss -tulpn` can connect a port to its responsible process.
- 🌐 Port 53 is commonly associated with DNS.
- 📡 `ping` tests basic reachability and response time.
- 🔎 `dig` allows DNS information to be inspected directly.
- 🚩 Unexpected connections and listening ports are investigation clues.
- 🔄 Repeated connections can resemble beaconing.
- 🧩 Process and network evidence become more useful when analyzed together.
- 🛡️ Network investigation can begin from the machine itself without relying only on Wireshark.

---

## 🎯 Final Takeaway

> **A security investigator doesn't just ask what is happening. They connect the evidence to understand why it is happening.**

Day 57 taught me to investigate:

**🧩 What is running?**

Day 58 taught me to investigate:

**🌐 What is it talking to?**

Day 59 will add:

**📜 What happened over time?**

The investigation is starting to come together:

**Processes → Network → Logs → Evidence → Investigation** 🔐

---

## 📚 Commands Covered

```bash
ss -tuln
netstat -tuln
sudo ss -tulpn
ping -c 4 example.com
dig example.com
```

**Day 58 complete. 🐧🔎🌐**
