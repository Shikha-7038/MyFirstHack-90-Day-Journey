# 🛡️ Day 15 – Phishing Email Analysis Project

**📅 Date:** August 7, 2026

## 🎯 Objective

Perform my first phishing email investigation using a structured workflow similar to that followed by a Tier 1 SOC (Security Operations Center) Analyst and document the findings in a professional incident report.

---

# 📝 Tasks Performed

## ✅ 1. Learned the Phishing Investigation Workflow

Understood the five main stages of a phishing investigation:

- Source a phishing email or phishing URL
- Analyse email headers (if available)
- Investigate URLs and attachments safely
- Identify social engineering techniques
- Prepare a SOC-style incident report

---

## ✅ 2. Selected a Phishing Sample

Since I could not find a suitable phishing email in my spam folder, I chose **Option C – PhishTank**.

I selected a verified phishing URL from the PhishTank database.

### Because I used PhishTank:

- Email headers were unavailable.
- SPF, DKIM and DMARC analysis could not be performed.
- The investigation focused mainly on URL analysis.

---

## ✅ 3. Investigated the Phishing URL

Collected important information including:

- Phishing URL
- Submission date
- Network information
- WHOIS records
- Domain registration details

### 📚 Learned

WHOIS records provide useful information such as:

- Domain creation date
- Registrar
- Name servers
- Expiration date
- Hosting details

---

## ✅ 4. Analysed the URL with VirusTotal

Submitted the phishing URL to VirusTotal.

### 🔍 Finding

VirusTotal reported:

> **No security vendors flagged this URL as malicious.**

Initially this was confusing because PhishTank had already verified the URL as phishing.

### 📚 Learned

Different security platforms use different:

- Threat intelligence feeds
- Detection engines
- Reputation databases

A phishing URL may already be identified on one platform while remaining undetected on another.

**Important lesson:** Never rely on a single security tool before reaching a conclusion.

---

## ✅ 5. Analysed the URL with URLScan.io

Submitted the phishing URL to URLScan.

### 🔍 Finding

URLScan returned:

> **HTTP 400 — DNS Error**

The domain could no longer be resolved.

### 📚 Learned

This does **not** necessarily mean the website is safe.

Many phishing websites are removed shortly after being reported.

Even when a phishing page becomes unavailable, its historical threat intelligence remains valuable for investigation.

---

## ✅ 6. Studied the Domain

Observed that:

- The URL structure was long and confusing.
- The domain attempted to appear legitimate.
- The actual domain differed from what users might expect.

### 📚 Learned

Always verify the **actual domain name** instead of trusting how a link appears visually.

---

## ✅ 7. Identified Social Engineering Techniques

The phishing sample mainly relied on:

### 🤝 Familiarity

- Attempted to appear trustworthy.

### 👤 Authority (Possible)

- Appeared related to an official organisation or service.

### ⏰ Urgency (Possible)

- Encouraged users to act quickly without carefully checking the destination.

### 📚 Learned

Phishing attacks succeed because they exploit **human psychology**, not just technical vulnerabilities.

---

## ✅ 8. Created a SOC-Style Phishing Analysis Report

Prepared my first professional phishing investigation report containing:

- Executive Summary
- Indicators of Compromise (IOCs)
- URL Analysis
- Domain Investigation
- Social Engineering Analysis
- Severity Assessment
- Recommended Actions

This was my first experience documenting a phishing investigation using a format similar to real SOC analysts.

---

# 📚 New Concepts Learned

- PhishTank
- VirusTotal
- URLScan.io
- WHOIS Lookup
- Indicators of Compromise (IOCs)
- Threat Intelligence
- Domain Reputation
- Social Engineering
- SOC Incident Reporting

---

# 💡 Practical Findings

- ✔ A phishing website can disappear shortly after being reported.
- ✔ VirusTotal and PhishTank may produce different results because they use different threat intelligence sources.
- ✔ One security tool alone should never determine the final verdict.
- ✔ Historical threat intelligence remains useful even if a phishing website is offline.
- ✔ Checking the actual domain is more important than trusting the visible text of a link.
- ✔ Effective phishing analysis combines technical investigation with understanding human behaviour.

---

# ⚠ Challenges Faced

- Could not find a phishing email in my spam folder.
- Used PhishTank instead of analysing a real email.
- Could not perform SPF, DKIM or DMARC analysis.
- Initially found it confusing that VirusTotal and PhishTank produced different results.
- Learned how to interpret findings from multiple tools before reaching a conclusion.

---

# 🚀 Key Takeaways

- Never click suspicious links during an investigation.
- Validate findings using multiple trusted security tools.
- Phishing investigations require both technical analysis and psychological understanding.
- Domain reputation is valuable but should never be the only deciding factor.
- Clear documentation is as important as identifying the threat itself.

---

# 🎯 Conclusion

Day 15 was my first hands-on phishing investigation project.

Rather than only learning about phishing attacks, I followed a structured investigation process similar to a Tier 1 SOC Analyst. I safely analysed a phishing URL, compared results from different security platforms, identified social engineering techniques, and documented the findings in a professional SOC-style report.

This project showed me that cybersecurity is not only about detecting threats—it is also about collecting evidence, validating information from multiple sources, and communicating findings through structured documentation.

-------

