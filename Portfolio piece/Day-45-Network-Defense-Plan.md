# Traffic Investigation Report

**Analyst:**  Shikha
**Analysis Date:**  6 September 2026
**Engagement:** Network Traffic Capture Investigation  
**Methodology:** Orient → Question → Filter → Follow → Compare → Document

---

## 1. Capture Summary

- **Source:** Wireshark sample capture `http_with_jpegs.cap`
- **Total packets:** 483
- **Time span:** 11 seconds (2004-11-20 03:59:14 to 03:59:25)

**Headline:** The capture contained HTTP web traffic, including HTML page requests and JPEG image transfers. The investigation found no clear evidence of the attack patterns checked, although unencrypted HTTP traffic was present.

## 2. Orientation

### Top protocols (from Protocol Hierarchy)

- IPv4 — 483 packets
- TCP — 464 packets
- HTTP — 39 packets

### Busiest conversation (from Conversations, sorted by bytes)

- **Conversation:** `10.1.1.101:3200 ↔ 10.1.1.1:80`
- **Packets:** 209
- **Data:** Approximately 204 KB
- **TCP Stream ID:** 18

### Notable endpoints

- `10.1.1.101`
- `10.1.1.1`
- No endpoint stood out as clearly anomalous based on the endpoint information examined.

## 3. Investigation

**Question investigated:** What is the main high-volume HTTP conversation, and does the traffic represent normal web activity or a suspicious network pattern?

### Filters used

```wireshark
http
http.response
tcp.stream eq 18
tcp.flags.reset == 1
dns
```

### Findings from following the thread

Following TCP Stream 18 revealed an HTTP GET request for a JPEG image. The server returned `HTTP/1.1 200 OK`, with `Content-Type: image/jpeg` and `Content-Length: 191515`. This explained the high volume of traffic in the busiest conversation. Other HTTP requests for HTML pages and images were also observed.

## 4. Comparison to Baseline

The traffic was assessed against normal-traffic patterns and the attack patterns checked during this investigation.

| Pattern / Indicator | Assessment | Evidence |
|---|---|---|
| Normal traffic | Observed | Following TCP Stream 18 revealed an HTTP request for a JPEG image and a successful `200 OK` response. The high-volume conversation was explained by the image transfer. |
| Port scan signature | Not observed by the check performed | The filter `tcp.flags.reset == 1` returned no packets, so the investigation did not find evidence of the classic port-scan pattern checked. This filter alone cannot rule out all port scans. |
| Suspicious DNS | Not observed in this capture | The filter `dns` returned no packets. No DNS traffic was available in this capture to support a suspicious-DNS finding. |
| Beacon pattern | Not observed | The IO Graph did not show a clear, regular beacon-like pattern of small connections at consistent intervals. |
| Plaintext exposure | Present | HTTP traffic was present instead of HTTPS, making the application-layer requests and responses readable in Wireshark. |
| Other / unexplained | No clear finding from the checks performed | The evidence examined did not reveal another clearly unexplained pattern. |

## 5. Verdict and Confidence

- **Verdict:** Normal traffic
- **Confidence:** PROBABLE

**Reasoning:** The evidence examined was consistent with ordinary HTTP web browsing and image retrieval. The busiest conversation was explained by a JPEG image transfer, and the specific checks performed did not reveal clear port-scanning, suspicious-DNS, or beaconing patterns.

Confidence is **PROBABLE** rather than **CERTAIN** because the capture contained multiple instances of `TCP Previous segment not captured`, indicating that some TCP segments may be missing. The conclusion is therefore limited to the traffic available for analysis. The absence of a pattern in this capture does not prove that no malicious activity occurred.

## 6. Recommended Next Steps

If this were a real engagement:

1. Investigate the external address `209.225.0.6` to determine whether the communication was expected and identify the service or application responsible.
2. Capture additional traffic from the same host if further evidence is required.
3. Check the external IP against reputable threat-intelligence sources and validate any matches with additional context.

---

**End of Report**
