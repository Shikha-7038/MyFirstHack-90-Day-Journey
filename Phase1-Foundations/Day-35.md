# Day 35 — Networks Capstone: Traffic Investigation

## Overview

Day 35 was the capstone of the Networks track. I brought together the Wireshark skills I developed throughout the week and investigated a real sample network traffic capture from beginning to end.

The goal was not to inspect every packet manually. Instead, I followed an analyst workflow:

**Orient → Question → Filter → Follow → Compare → Document**

I used the public Wireshark sample capture **`http_with_jpegs.cap`** and investigated whether the traffic contained anything suspicious.

---

## Objectives

- Understand an unfamiliar packet capture before filtering it.
- Use Wireshark's Statistics tools to identify important protocols, conversations, and endpoints.
- Form a specific investigation question.
- Use display filters to narrow the investigation.
- Follow a TCP conversation and understand the application-layer traffic.
- Compare observed traffic with normal-traffic and attack patterns.
- Document findings clearly and state confidence honestly.

---

## Capture Summary

| Item | Finding |
|---|---|
| Capture | `http_with_jpegs.cap` |
| Total packets | 483 |
| First packet | 2004-11-20 03:59:14 |
| Last packet | 2004-11-20 03:59:25 |
| Time span | 11 seconds |
| Main protocol activity | IPv4, TCP, HTTP |

The capture contained HTTP web traffic, including requests for HTML pages and JPEG images.

---

## 1. Orientation

I first used Wireshark's **Statistics** menu to understand the overall shape of the capture before investigating individual packets.

### Protocol Hierarchy

The main protocols by packet count were:

1. **IPv4 — 483 packets**
2. **TCP — 464 packets**
3. **HTTP — 39 packets**

This showed that the capture was primarily IPv4/TCP traffic with HTTP application traffic.

### Busiest Conversation

The busiest conversation I identified was:

```text
10.1.1.101:3200 ↔ 10.1.1.1:80
```

- Packets: **209**
- Data: approximately **204 KB**
- TCP Stream ID: **18**

This conversation became the main thread for my investigation.

### Endpoints

The main endpoints observed were:

- `10.1.1.101`
- `10.1.1.1`

No endpoint stood out as clearly anomalous based on the endpoint information I examined.

---

## 2. Investigation Question

I chose the following question:

> **What is the main high-volume HTTP conversation, and does the traffic represent normal web activity or a suspicious network pattern?**

I focused on the busiest conversation because it contained significantly more packets and data than the smaller conversations.

---

## 3. Filters Used

I used Wireshark display filters to narrow the investigation:

```text
http
```

Used to focus on HTTP traffic.

```text
http.response
```

Used to identify HTTP responses.

```text
tcp.stream eq 18
```

Used to isolate the busiest TCP conversation.

I also used the following filters when comparing the traffic with known attack patterns:

```text
tcp.flags.reset == 1
```

Used to check for a possible port-scan pattern.

```text
dns
```

Used to check for DNS activity and possible suspicious DNS behavior.

---

## 4. Following the TCP Stream

Following **TCP Stream 18** was the most useful part of the investigation.

The stream showed an HTTP request for a JPEG image:

```http
GET /Websidan/2004-07-SeaWorld/fullsize/DSC07858.JPG HTTP/1.1
```

The server returned:

```text
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 191515
```

The large amount of traffic in the conversation was therefore explained by the transfer of a JPEG image.

I also observed other HTTP GET requests for normal-looking web content, including HTML pages and smaller images.

---

## 5. Comparison to Normal and Attack Patterns

I compared the traffic against patterns studied earlier in the Networks track.

### Port Scan

Filter:

```text
tcp.flags.reset == 1
```

**Result:** No packets were returned.

Therefore, I did not observe evidence of the classic port-scan pattern of one source sending connection attempts to many ports and receiving large numbers of resets.

### Suspicious DNS

Filter:

```text
dns
```

**Result:** No packets were returned.

There was therefore no DNS traffic in the capture to support a suspicious-DNS finding.

### Beaconing

I checked the traffic pattern using Wireshark's IO Graph.

I did not observe a clear, regular beacon-like pattern of small connections occurring at consistent intervals.

### Plaintext Exposure

HTTP traffic was present instead of HTTPS.

The capture therefore contained **unencrypted HTTP traffic**, and the HTTP requests and responses were readable in Wireshark.

This is a security observation, but it is not by itself evidence that an attack occurred.

---

## 6. Findings

### Finding 1 — Normal HTTP web activity

The investigated traffic contained HTTP GET requests for HTML pages and JPEG images. Successful `HTTP/1.1 200 OK` responses were observed.

### Finding 2 — High-volume conversation explained

The busiest conversation contained 209 packets and approximately 204 KB of traffic. Following the TCP stream showed that the traffic was largely explained by a JPEG image transfer.

The response contained:

```text
Content-Type: image/jpeg
Content-Length: 191515
```

### Finding 3 — No clear attack signature observed

The investigation did not identify a clear:

- Port scan
- Suspicious DNS pattern
- Beaconing pattern
- Other obvious malicious network behavior

### Finding 4 — HTTP plaintext exposure

The capture used HTTP rather than HTTPS, so application-layer requests and responses were transmitted without TLS encryption.

---

## 7. Verdict and Confidence

**Verdict:** Normal traffic

**Confidence:** PROBABLE

### Reasoning

The evidence examined is consistent with ordinary HTTP web browsing and image retrieval. The high-volume conversation was explained by the transfer of a JPEG image, and the HTTP responses returned successful `200 OK` status codes.

The specific checks performed did not reveal a clear port-scan, suspicious DNS, or beaconing pattern.

I used **PROBABLE** rather than CERTAIN because the capture contained multiple instances of **“TCP Previous segment not captured”**, meaning that some TCP segments may be missing from the recorded capture. Therefore, the conclusion is limited to the traffic that was available for analysis.

---

## 8. Analyst Mindset

One important lesson from this investigation was the importance of not forcing the evidence to fit an attack.

Because I was investigating network traffic as a cybersecurity exercise, it would have been easy to assume that unusual or unfamiliar traffic must be malicious.

Instead, I followed the evidence:

**Question → Filter → Follow → Read → Compare → Conclude**

The large conversation initially looked worth investigating, but following the stream provided a normal explanation: a JPEG image transfer.

A finding of **“normal traffic, no suspicious activity observed”** is still a valid security investigation result.

---

## 9. What I Would Investigate Further

If this were a real engagement, I would investigate the communication with the external address:

```text
209.225.0.6
```

I would determine whether this destination was expected for the environment and identify what service or application was responsible for the communication.

I would also capture additional traffic from the same host if more evidence were required.

---

## 10. Most Useful Wireshark Feature

The most useful feature for me today was:

### Follow TCP Stream

It allowed me to move from individual packets to the complete conversation and understand what the communication was actually doing.

In this investigation, it helped explain why the busiest conversation contained approximately 204 KB of traffic.

---

## 11. Day 26 vs Day 35

Day 26 focused on **network reconnaissance and footprint mapping**.

Day 35 felt more like real security operations work because I had to investigate an unfamiliar dataset, decide what was worth examining, follow evidence, compare it with known patterns, and make a conclusion based on the available evidence.

The process was closer to the type of investigation a SOC or network analyst might perform when reviewing suspicious network activity.

---

## Key Takeaways

- Do not try to read every packet in a large capture.
- Start with **orientation** before filtering.
- Use **Protocol Hierarchy, Conversations, and Endpoints** to understand the capture.
- Form a specific question instead of investigating randomly.
- Use display filters to narrow the investigation.
- **Follow TCP Stream** when a conversation is the important thread.
- Compare traffic against normal baselines and known attack patterns.
- HTTP traffic is plaintext and should be distinguished from encrypted HTTPS traffic.
- Missing packets can reduce confidence in an investigation.
- Not finding an attack is a valid finding.
- Good analysts report what the evidence supports rather than forcing a dramatic conclusion.

---

## Portfolio Artifact

**Artifact:** Traffic Investigation Report  
**Track:** Networks  
**Day:** 35  
**Tool:** Wireshark  
**Investigation type:** Network traffic / packet analysis

This is the second Networks-track portfolio artifact, following the **Network Footprint Report from Day 26**.

---

## Final Summary

Day 35 brought the Networks track together into one complete investigation workflow.

I started with an unfamiliar packet capture, established its overall shape, identified the busiest conversation, formed an investigation question, filtered and followed the relevant TCP stream, examined the HTTP requests and responses, compared the traffic with known attack patterns, and documented the result.

The investigation concluded that the traffic examined was **probably normal HTTP web activity**, with plaintext HTTP exposure but no clear evidence of the attack patterns checked.
