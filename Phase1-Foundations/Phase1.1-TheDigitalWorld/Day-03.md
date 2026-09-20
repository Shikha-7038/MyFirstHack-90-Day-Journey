# 📅 Day 3 – Personal Security Audit

**📅 Date:** 26 July 2026

---

# 🎯 Objective

The objective of today's lesson was to understand what a security audit is, learn the standard audit methodology used by cybersecurity professionals, and perform my first personal security audit on my own digital accounts and devices.

Unlike previous lessons that focused mainly on concepts, today's lesson emphasized practical application by conducting a structured security assessment.

---

# 📖 What is a Security Audit?

A security audit is a structured process used to identify the gap between the current security of a system and the level of security it should have.

Instead of making assumptions, an auditor:

- Defines the scope
- Collects information
- Identifies weaknesses
- Rates the severity of findings
- Applies or recommends security improvements

I also learned that this methodology is commonly used by both:

- **SOC Analysts** to identify signs of compromise
- **GRC Analysts** to identify governance, risk, and compliance issues

Although their objectives differ, both roles follow a structured audit process.

---

# 🛠️ The Five-Step Audit Methodology

## 📌 1. Scope

The first step of any audit is defining what will be assessed.

For my audit, I included:

- Gmail
- Google Account
- LinkedIn
- Amazon
- GitHub
- Windows Laptop
- Android Phone
- Primary Wi-Fi Network

This helped me understand that an audit cannot begin until the target systems are clearly defined.

---

## 🔍 2. Intelligence

This phase focuses on gathering publicly available information before looking for weaknesses.

### 🌐 Have I Been Pwned

I checked my primary email address.

**Result**

- No known public data breaches were found.

This indicated that my primary email has not appeared in any publicly known breach database.

### 🌐 Epieos

I searched the same email using Epieos.

The tool associated my email with:

- Adobe
- Spotify
- Smule

Initially, I assumed this meant those accounts had been compromised.

After learning more about OSINT, I realized this only indicates that my email is associated with these services and **does not mean the accounts have been hacked.**

This was an important lesson about understanding OSINT results correctly.

---

# 🌍 What I Learned About OSINT

Today's lesson showed me that attackers often begin by collecting publicly available information instead of immediately attacking systems.

A single email address can reveal:

- Online services
- Public account information
- Profile images

This highlighted the importance of understanding my own digital footprint.

---

## 🚨 3. Exposure Assessment

This phase focused on identifying my current security risks.

### 💻 Active Sessions

I reviewed every device currently signed into my Google account.

**Recognized devices**

- Windows Laptop
- Android Phone

**Unknown devices**

- None

This confirmed there were no suspicious active sessions.

---

### 🔐 Two-Factor Authentication Review

I reviewed the security settings of my important accounts.

| Account | 2FA Status |
|----------|------------|
| Gmail | ON |
| Google | OFF |
| LinkedIn | OFF (before remediation) |
| Amazon | SMS Only |
| GitHub | ON |

One important lesson I learned was that SMS-based verification is generally weaker than authenticator app-based verification.

---

### 🔑 The "Master Key" Concept

One of today's biggest takeaways was understanding why an email account is considered the **master key**.

I estimated that approximately **6 accounts** could be reset if someone gained access to my primary email account.

This completely changed how I think about protecting my email account.

---

## ⚖️ 4. Severity Assessment

I learned that every finding should be prioritized according to its impact.

My findings included:

- No public data breaches
- No unknown active sessions
- Email associated with Adobe, Spotify, and Smule through OSINT
- LinkedIn account without 2FA before remediation

Instead of treating every issue equally, I learned to classify them by severity.

---

## ✅ 5. Remediation

Every audit should end with action.

Based on my findings, I immediately improved my account security by:

- Enabling Two-Factor Authentication (2FA) on my LinkedIn account

This demonstrated that a security audit should produce practical improvements, not just observations.

---

# 🚧 Challenges Faced

During this activity, I encountered several questions that helped deepen my understanding.

- I was unsure whether creating a free Epieos account was safe.
- I initially misunderstood the Epieos results and thought the associated services meant my accounts had been compromised.
- I found the "Master Key" question confusing before understanding that it refers to password recovery through a primary email account.

Researching these questions helped me better understand the concepts instead of simply following the instructions.

---

# 💻 Skills Practiced

- Security Auditing
- Open Source Intelligence (OSINT)
- Digital Footprint Analysis
- Two-Factor Authentication Review
- Risk Assessment
- Severity Classification
- Security Remediation
- Technical Documentation

---

# 📚 Key Takeaways

- A professional security audit follows five structured phases:
  - Scope
  - Intelligence
  - Exposure
  - Severity
  - Remediation

- OSINT tools can reveal publicly available information linked to an email address.
- My primary email has not appeared in any known public data breaches.
- My Google account contained only recognized active sessions.
- My primary email functions as the recovery point for several important accounts, making it one of the most critical accounts to protect.
- Not every security finding has the same level of risk; prioritization is an essential part of an audit.
- A security audit should always conclude with a practical security improvement.

---

# 🏁 Conclusion

Day 3 marked my first experience performing a structured cybersecurity assessment instead of only studying theory.

By auditing my own digital security, documenting findings, assessing risk, and implementing a remediation step, I gained practical experience in how security professionals approach security assessments.

This project also became the first artifact in my cybersecurity portfolio and reinforced the importance of structured thinking, documentation, and continuous improvement in cybersecurity.

---

# 📄 Portfolio Artifact

## Personal Security Audit Report

> **Note:** This is a privacy-safe version of my personal security audit report. Personal information such as my email address, network details, and identifiable account information has been removed or generalized.

---

# 👤 Auditor Information

| Field | Details |
|-------|---------|
| **Auditor** | Shikha |
| **Audit Date** | 26 July 2026 |
| **Engagement** | Personal Digital Security Assessment |
| **Methodology** | Scope → Intelligence → Exposure → Severity → Remediation |

---

# 🎯 1. Scope

## Systems and Accounts Assessed

- **Primary Email:** `[REDACTED]`
- **Key Accounts:**
  - Google
  - Gmail
  - LinkedIn
  - Amazon
  - GitHub
- **Primary Devices:**
  - Windows Laptop
  - Android Phone
- **Network:** `[REDACTED]`

---

# 📋 2. Executive Summary

A personal security assessment was conducted to evaluate the security of my primary digital accounts and devices.

No known public data breaches or unrecognized active sessions were identified during the assessment. The audit highlighted several opportunities to strengthen account security, particularly by improving two-factor authentication (2FA) settings.

One security improvement was implemented immediately by enabling 2FA on my LinkedIn account.

---

# 🔍 3. Findings

## 🔴 Critical

- Primary Google account does not currently use app-based two-factor authentication.

---

## 🟠 High

- LinkedIn account did not have two-factor authentication enabled at the time of assessment (**remediated during this audit**).
- Approximately **six important accounts** could potentially be reset if an attacker gained access to my primary email account, highlighting the importance of protecting the primary email account.

---

## 🟡 Medium

- OSINT analysis revealed that my email address is associated with **multiple online services**, demonstrating my publicly visible digital footprint.
- Amazon currently uses **SMS-based two-factor authentication**, which provides weaker protection than an authenticator application.

---

## 🟢 Low

- No known public data breaches were found for my primary email address.
- No unrecognized active sessions were detected. Only my recognized Windows laptop and Android phone were signed in.

---

# ✅ 4. Actions Taken During Audit

- ✅ Enabled Two-Factor Authentication (2FA) on my LinkedIn account.

---

# 🛠️ 5. Remediation Plan

## 📅 This Week

- Upgrade my Google account to app-based two-factor authentication.
- Replace SMS-based 2FA on Amazon with an authenticator app (if supported).
- Review password recovery options for my important accounts.

---

## 📆 This Month

- Review accounts associated with my primary email and remove unused accounts where appropriate.
- Review passwords and ensure each important account has a strong, unique password.
- Repeat this personal security audit to measure security improvements.

---

# 🏁 Conclusion

This audit provided practical experience in applying a structured cybersecurity audit methodology.

Rather than only studying security concepts, I assessed my own digital environment, identified potential risks, prioritized findings based on severity, and implemented an immediate remediation.

The exercise reinforced the importance of protecting a primary email account, understanding digital exposure through OSINT, and following a systematic approach to improving personal security.