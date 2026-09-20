# Day 36 — IDS, IPS & Detection Rules

## 📌 Topic
**Intrusion Detection Systems (IDS), Intrusion Prevention Systems (IPS), Detection Rules & False Positives**

---

## 🎯 Objective

Today I learned how organisations automatically monitor network traffic for suspicious activity using **IDS and IPS**, how detection rules identify known attack patterns, and why handling **false positives** is one of the biggest challenges in security monitoring.

I also explored real Snort detection rules and connected one of them to the port-scanning concepts I learned earlier.

---

## 🔍 1. Why Manual Traffic Investigation Doesn't Scale

Previously, I investigated network traffic manually using packet-analysis techniques.

Manual investigation is useful for understanding what is happening in a network, but it cannot scale to a real organisation.

A busy network can generate millions or even billions of packets, making it impossible for a human to inspect everything continuously.

This is why organisations use automated detection systems.

---

## 🛡️ 2. IDS — Intrusion Detection System

An **IDS** monitors network traffic and looks for suspicious activity.

When it detects something suspicious, it generates an **alert** for a security analyst to investigate.

A network-based IDS commonly receives a copy of network traffic through mechanisms such as a network tap or switch port mirroring.

### Simple analogy

**IDS = Smoke detector**

It detects a problem and raises an alarm, but it does not directly stop the traffic.

### IDS workflow

```text
Network Traffic
       ↓
      IDS
       ↓
Suspicious activity?
       ↓
      YES
       ↓
🚨 Alert
       ↓
SOC Analyst investigates
```

---

## 🚧 3. IPS — Intrusion Prevention System

An **IPS** also detects suspicious activity, but it is placed **inline** with network traffic.

Because traffic passes through the IPS, it can take action when it detects malicious activity.

Depending on its configuration, an IPS may:

- Drop malicious packets
- Reset connections
- Block a source
- Prevent suspicious traffic from reaching its destination

### Simple analogy

**IPS = Sprinkler system**

It detects the problem and can also take action to stop it.

### IPS workflow

```text
Network Traffic
       ↓
      IPS
       ↓
Inspect traffic
       ↓
Malicious?
       ↓
      YES
       ↓
🛑 Block
```

---

## ⚖️ 4. IDS vs IPS

| Feature | IDS | IPS |
|---|---|---|
| Full form | Intrusion Detection System | Intrusion Prevention System |
| Position | Usually monitors a copy of traffic | Inline with traffic |
| Detects threats | ✅ | ✅ |
| Generates alerts | ✅ | ✅ |
| Automatically blocks | ❌ | ✅ |
| Main purpose | Detect and report | Detect and prevent |
| Risk of false positive | Wasted investigation time | Can block legitimate traffic |

### Key difference

> **IDS detects and alerts; IPS detects and can block.**

---

## 🔎 5. How IDS/IPS Detect Malicious Activity

There are two major detection approaches.

### A. Signature-Based Detection

Signature-based detection looks for **known patterns associated with attacks**.

It is similar to antivirus software recognising known malware.

For example:

```text
Network Traffic
      ↓
Compare with known signatures
      ↓
Pattern matches?
      ↓
🚨 Alert
```

### Advantages

- Fast
- Precise for known threats
- Usually produces fewer false positives

### Limitation

It may not detect a completely new attack for which no signature exists.

This includes **zero-day attacks**.

---

### B. Anomaly-Based Detection

Anomaly-based detection learns what **normal behaviour** looks like and looks for significant deviations.

This connects to the baseline concept I learned earlier.

Example:

```text
Normal:
Server → communicates with 10 systems

Suddenly:
Server → communicates with 10,000 systems
```

The unusual behaviour may trigger an alert.

### Advantages

- Can detect previously unknown or unusual activity
- Useful for identifying behaviour that does not match known signatures

### Limitation

Unusual does not always mean malicious.

Legitimate activity can also trigger an alert, creating **false positives**.

---

## 🧪 6. Exploring Real Snort Detection Rules

As part of today's lab, I examined real Snort rules to understand how signature detection works.

### Rule 1

```text
alert tcp $EXTERNAL_NET 80 -> $HOME_NET any (
    msg:"Attack attempt!";
    flow:to_client,established;
    file_data;
    content:"1337 hackz 1337",fast_pattern,nocase;
    service:http;
    sid:1;
)
```

### Plain-English interpretation

This rule examines TCP/HTTP traffic and looks for the specific content pattern:

```text
1337 hackz 1337
```

If the required conditions match, Snort generates an alert.

### Detection approach

**Signature-based**

The rule searches for a specific known pattern rather than determining whether the traffic is simply unusual.

---

### Rule 2

```text
alert http (
    msg:"SERVER-WEBAPP This rule only looks at HTTP traffic";
    flow:to_server,established;
    http_uri;
    content:"/admin.php",fast_pattern,nocase;
    content:"cmd=",nocase;
    pcre:"/[?&]cmd=[^&]*?\x3b/i";
    sid:1;
)
```

### Plain-English interpretation

This rule looks at HTTP requests and checks for a specific combination of characteristics, including:

- `/admin.php`
- `cmd=`
- An additional regular-expression pattern

If the required conditions match, Snort generates an alert.

### Detection approach

**Signature-based**

It looks for a specific suspicious web-request pattern.

---

## 🔬 7. Connecting Detection Rules to Day 33

I also examined a Snort scan-detection example related to **network scanning**.

The rule included conditions such as:

```text
flags:S;
```

which checks for the TCP **SYN flag**, along with other conditions associated with a scanner.

It was classified as:

```text
attempted-recon
```

### Connection to Day 33

On Day 33, I learned that attackers can use **port scanning** to discover open ports and services on a target.

The detection rule shows how a security system can use specific characteristics of network traffic to identify activity associated with reconnaissance.

### Detection approach

**Signature-based detection**

The example looks for a specific combination of packet characteristics associated with a known scanning pattern.

> Note: General port-scan detection can also involve behavioural analysis, such as observing many connection attempts across ports over time. Therefore, not every form of port-scan detection is purely signature-based.

---

# 🚨 8. The False Positive Problem

A **false positive** occurs when a security system generates an alert for activity that is actually legitimate.

Example:

```text
Normal backup
     ↓
Large amount of data transferred
     ↓
IDS sees unusual activity
     ↓
🚨 Alert
     ↓
But it was only a backup
```

If an IDS produces thousands of unnecessary alerts, analysts may become overwhelmed.

This can lead to **alert fatigue**.

### Alert fatigue

Alert fatigue happens when analysts receive so many alerts that it becomes difficult to identify the truly important ones.

This creates a dangerous situation:

```text
Thousands of alerts
        ↓
Lots of harmless activity
        ↓
Real attack hidden in the noise
        ↓
⚠️ Analyst may miss it
```

---

# 🎯 9. Block Automatically or Alert a Human?

For the lab, I considered four situations and evaluated them based on **confidence in the detection** and the **cost of being wrong**.

| Situation | Decision | Reasoning |
|---|---|---|
| Traffic matching a well-known, unambiguous ransomware signature | 🛑 **Block automatically** | The detection is highly specific and the potential damage from allowing ransomware through is severe. |
| Host suddenly making far more DNS queries than its normal baseline | 🚨 **Alert a human** | The behaviour is unusual but could have legitimate causes, so it should be investigated first. |
| Connection attempts to a port that should never be open | 🛑 **Block automatically** | If the network policy clearly prohibits the port, blocking the connection has relatively low risk. |
| Internal host communicating with an IP in a country the business has no dealings with | 🚨 **Alert a human** | Geographic location alone does not prove malicious activity and legitimate services may use unexpected locations. |

---

# ⚠️ 10. False-Positive Examples

### High DNS activity

Automatic blocking could interfere with legitimate software updates, applications, browsing, or automated processes that temporarily generate many DNS requests.

### Unexpected country

Automatic blocking could interrupt legitimate cloud services, VPNs, CDNs, or third-party services whose infrastructure is located in an unexpected country.

---

# 🧠 11. Why Human Analysts Remain Essential

Security tools can identify suspicious patterns, but they cannot always understand the **business context** behind an event.

A human analyst can investigate:

- Is the activity actually malicious?
- Is this normal for this particular device?
- Is the destination legitimate?
- Was there another related security event?
- Should the activity be blocked?
- Is the alert a false positive?

Therefore:

> **Automated detection helps find suspicious activity at scale, but human analysts are still essential for deciding what the activity actually means and how to respond.**

---

# 🏪 12. Real-World Deployment

Some well-known network security tools include:

- **Snort** — classic open-source IDS/IPS
- **Suricata** — high-performance open-source IDS/IPS
- **Zeek** — network security monitoring and rich network activity logging

In larger organisations, IDS/IPS capabilities are also commonly integrated into security appliances such as next-generation firewalls.

Host-based intrusion detection also exists.

### HIDS — Host-Based Intrusion Detection System

A HIDS monitors activity on an individual computer or server, such as:

- Unexpected file changes
- Suspicious processes
- Other signs of compromise

This complements network-based detection.

---

# 🔗 13. Connection to My Previous Learning

Today's topic connects several earlier concepts:

```text
Day 32
Understand normal traffic
        ↓
Day 33
Recognise attack patterns
        ↓
Day 35
Investigate traffic manually
        ↓
Day 36
IDS/IPS automate detection
        ↓
False positives
        ↓
Too many alerts
        ↓
SIEM
        ↓
SOC investigation
```

This helped me understand that the packet analysis I learned manually is not separate from real security operations.

**I was learning the same detection concepts that automated security systems use, but at a much smaller scale.**

---

# 📌 Key Takeaways

- **IDS detects and alerts.**
- **IPS detects and can block traffic automatically.**
- IDS generally monitors a copy of traffic, while IPS operates inline.
- **Signature-based detection** looks for known attack patterns.
- **Anomaly-based detection** looks for behaviour that differs from the normal baseline.
- A false positive occurs when legitimate activity is incorrectly flagged as suspicious.
- Too many false positives can cause **alert fatigue**.
- Automatic blocking should be used carefully because a false positive can disrupt legitimate users or business activity.
- Human analysts remain essential for investigating alerts and determining whether suspicious activity is actually malicious.
- Snort, Suricata, and Zeek are important names to know in network security.
- The next step is understanding how **SIEM systems manage and correlate large numbers of security events**.

---

## 💡 Today's Lesson

> **The goal of security monitoring isn't to generate the most alerts — it's to generate the right alerts and make sure the important ones don't get lost in the noise.**