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