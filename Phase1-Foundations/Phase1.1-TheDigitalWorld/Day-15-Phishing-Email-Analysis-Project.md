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

# 📑 SOC-Style Phishing Analysis Report

## 📋 Basic Information

| Field | Details |
|-------|---------|
| **Analyst** | Shikha |
| **Analysis Date** | August 7, 2026 |
| **Engagement** | Suspected Phishing URL Investigation |
| **Methodology** | PhishTank → WHOIS → VirusTotal → URLScan.io → Social Engineering Analysis → Final Report |

---

## 1️⃣ Incident Summary

Since I could not find a suitable phishing email in my spam folder, I used a **verified phishing URL from PhishTank** for this investigation.

The investigation focused on analysing the phishing URL, domain registration details, threat intelligence results, and the social engineering techniques used by the attacker.

Although the phishing page was no longer accessible during the investigation, historical threat intelligence confirmed it had previously been identified as a phishing campaign.

---

## 2️⃣ Indicators of Compromise (IOCs)

| Indicator | Observation |
|-----------|-------------|
| **Phishing URL** | `https://dupplacidadania.com/wp-admin/js/widgets/membercenter.made-in-china.com/index.html` |
| **Hosting Network** | Oracle Corporation (AS31898) |
| **Domain** | dupplacidadania.com |
| **Registrar** | PublicDomainRegistry (PDR Ltd.) |
| **Creation Date** | March 30, 2023 |
| **Status During Analysis** | Offline (DNS Resolution Error) |

---

## 3️⃣ Email Header Analysis

Since this investigation was performed using **PhishTank (Option C)** instead of a real phishing email, email header analysis could not be completed.

| Field | Result |
|-------|--------|
| SPF | Not Available |
| DKIM | Not Available |
| DMARC | Not Available |
| Sender Address | Not Available |
| Received Headers | Not Available |

**Reason:** The original phishing email was not available, so email authentication results could not be analysed.

---

## 4️⃣ Domain Investigation

| Item | Observation |
|------|-------------|
| Domain | dupplacidadania.com |
| Registrar | PublicDomainRegistry |
| Hosting Provider | Oracle Corporation |
| DNSSEC | Unsigned |
| Domain Age | Created in March 2023 |

### Findings

- WHOIS successfully revealed the domain registration information.
- The phishing URL used a long and confusing path.
- The actual domain differed from what many users might assume.
- A legitimate registrar does **not** guarantee a legitimate website.

---

## 5️⃣ URL Analysis

### 🔹 VirusTotal

**Result**

- No security vendors flagged the URL as malicious.

**Observation**

Even though VirusTotal reported no detections, the URL had already been verified as phishing by PhishTank.

**Learning**

Different threat intelligence platforms collect and update data independently. Analysts should compare results from multiple trusted tools before making a final decision.

---

### 🔹 URLScan.io

**Result**

HTTP 400 Error
DNS Error – Could not resolve domain


**Observation**

The phishing website was no longer accessible.

**Learning**

Phishing websites are often removed or become inactive shortly after being reported. Historical threat intelligence is still valuable even after a phishing page disappears.

---

## 6️⃣ Social Engineering Analysis

### Techniques Identified

- ✅ Familiarity
- ✅ Authority (Possible)
- ✅ Urgency (Possible)

### Explanation

The phishing URL attempted to appear trustworthy and encourage users to interact with it without carefully checking the destination.

The attack relied more on manipulating user trust than exploiting technical vulnerabilities.

### Likely Target

- General internet users
- Non-technical users
- Users unfamiliar with identifying suspicious URLs

---

## 7️⃣ Severity Assessment

**Severity:** 🟠 Medium

### Justification

The phishing URL had already been confirmed by PhishTank, indicating that it was part of a real phishing campaign.

Although the page was offline during analysis, the URL structure and threat intelligence suggested it had been designed to deceive users into visiting a malicious website.

---

## 8️⃣ Recommended Actions

### For Individual Users

- Never click suspicious links directly.
- Verify the actual domain before entering credentials.
- Enable Multi-Factor Authentication (MFA).
- Report phishing attempts instead of interacting with them.

### For Organisations

- Block known phishing domains.
- Use multiple threat intelligence sources during investigations.
- Conduct regular phishing awareness training.
- Monitor newly reported phishing campaigns.

---

## 🎯 Final Verdict

| Field | Result |
|------|--------|
| **Classification** | Phishing |
| **Confidence** | High |
| **Severity** | Medium |

### Conclusion

This investigation demonstrated that phishing analysis involves much more than checking whether a URL is online.

One of the biggest lessons I learned was that **security analysts should never rely on a single security tool**. VirusTotal, PhishTank, WHOIS, and URLScan.io each contributed different evidence, and combining these findings resulted in a more accurate assessment.

This project also reinforced that successful phishing attacks rely heavily on **social engineering**, making user 