# Day 17 – Understanding Cloud Security and Internet Exposure

📅 **Date:** 09-08-2026  
🚀 **Journey:** Day 17 of 90 – MyFirstHack

---

## 🎯 Today's Objective

Today I learned what **"the cloud"** actually means from a cybersecurity perspective.

Instead of thinking about the cloud as something completely separate from normal computers, I understood that cloud services are computing resources and data centres operated by companies such as **AWS, Microsoft, and Google**.

### What I focused on

- ☁️ What cloud computing actually means
- 🏢 Major cloud providers
- 🧩 Compute, storage, IAM and networks
- 🔐 The Shared Responsibility Model
- 💥 How cloud misconfigurations can lead to major breaches
- 🔎 How attackers discover publicly exposed systems
- 📱 How much cloud infrastructure my own digital life depends on
- 🛡️ Why MFA and proper access control matter

---

## ☁️ What I Learned About the Cloud

The first thing that became clear to me was that **the cloud is not something mysterious**.

A simple way I understood it is:

> The cloud is essentially someone else's computer and infrastructure that I access through the internet.

Instead of owning the physical hardware myself, companies such as Amazon, Microsoft and Google provide the infrastructure and services.

This helped me connect cloud security with concepts I have already learned:

- 🌐 Networks
- 🖥️ Servers
- 💾 Storage
- 🔑 Authentication
- 👤 Permissions
- 🔥 Firewalls
- 📋 Logging

The difference is that these systems can operate at a much larger scale.

---

## 🏢 Major Cloud Providers

I learned about:

- **Amazon Web Services (AWS)**
- **Microsoft Azure**
- **Google Cloud Platform (GCP)**

### Important AWS Terms

| Service | What I learned |
|---|---|
| **EC2** | Virtual computing instances |
| **S3** | Object storage |
| **IAM** | Identity and Access Management |
| **VPC** | Virtual Private Cloud |
| **CloudTrail** | Activity and audit logging |

I don't need to memorize every cloud service right now. My goal is to recognize these terms when I see them in cloud security reports or real incidents.

---

## 🔐 Shared Responsibility Model

One of the most important concepts today was the **Shared Responsibility Model**.

The cloud provider is generally responsible for the **security of the cloud infrastructure**, such as:

- 🏢 Physical data centres
- 🖥️ Hardware
- ⚙️ Underlying infrastructure
- 💻 Virtualization
- 🌐 Provider-managed systems

The customer is responsible for **security in the cloud**, depending on the service being used.

This includes:

- 🔑 Account security
- 👤 IAM permissions
- 💾 Data access
- ⚙️ Configurations
- 💻 Application security
- 🌐 Network rules
- 🔐 Secrets and credentials

### 💡 My Understanding

> Using a secure cloud provider does not automatically make the customer's cloud environment secure.

---

## 💥 Capital One Breach – What I Learned

The Capital One breach helped me understand why cloud configuration matters.

The important part for me was **how the attack happened**, rather than only the amount of data exposed.

The attack involved a chain of weaknesses:

**Misconfiguration → SSRF → Temporary Credentials → Excessive IAM Permissions → Access to Storage → Data Exfiltration**

This taught me that a serious security incident does not always require one huge vulnerability.

Several smaller weaknesses can combine into a major attack path.

### 🔑 Principle I Learned: Least Privilege

> A system or user should have only the permissions it actually needs.

---

# 🔎 My Personal Cloud Audit

I mapped the cloud services that I personally use.

I identified **14 services/accounts** and checked their MFA status.

Some services I reviewed included:

- 📧 Gmail
- 🎓 College email
- 📁 Google Drive
- 🖼️ Google Photos
- 💬 WhatsApp
- ✈️ Telegram
- 📸 Instagram
- 💼 LinkedIn
- 👻 Snapchat
- 💻 GitHub
- 🤖 ChatGPT
- 💳 Paytm
- 📈 Groww
- 🛒 Amazon

---

## 🔑 What I Learned About MFA and Google Login

One important thing I learned was:

> **Using a Gmail/Google account to sign in to another service does not automatically mean that the other service has its own MFA enabled.**

Google can protect my Google account with its own authentication methods, while another application can separately provide its own MFA.

So I started checking the security settings of important services individually instead of assuming that one security setting protects everything.

---

## 🛡️ MFA Findings and Remediation

During the audit, I found important accounts where MFA was not enabled.

Instead of only recording the findings, I **fixed the issues**.

I enabled MFA on accounts including:

- 🎓 College email
- 🤖 ChatGPT
- 💳 Paytm
- 🛒 Amazon
- 👻 Snapchat
- ✈️ Telegram
- And other accounts identified during the audit

After completing the changes:

> ✅ **All 14 services I checked had MFA enabled.**

This was one of the most useful parts of today's audit because I didn't just identify a security weakness — **I actually remediated it.**

### 💡 My Lesson

> A security audit is more useful when it leads to an actual security improvement.

---

# 🌐 Shodan – Seeing the Internet From an Attacker's Perspective

The second major practical activity was using **Shodan**.

Shodan helped me understand:

> **What can an attacker learn just by looking at systems that are already exposed to the internet?**

I only observed information already indexed by Shodan. I did **not** attempt to log in, access, scan, or interact with the devices.

---

## 🔎 Shodan Search 1 – MikroTik

I searched for:

```text
Mikrotik
```

Shodan showed:

**2,836,955 results**

The country with the highest number of results was:

🇨🇳 **China – 425,034**

Some common ports included:

- **161** – SNMP
- **8291** – MikroTik WinBox
- **1723** – PPTP
- **21** – FTP
- **80** – HTTP

One result showed:

```text
SNMP
Description: RouterOS x86
Name: MikroTik
Enterprise Name: MikroTik
```

This showed me that a publicly reachable service can reveal information about the type of device and software running on it.

I also learned that a **banner/service response** is information returned by a service that can help identify the technology running on a system.

---

## 🔎 Shodan Search 2 – Telnet

I searched:

```text
country:US port:23
```

The result showed:

**57,820 results**

Port **23** is commonly associated with **Telnet**.

What surprised me was seeing such a large number of publicly indexed systems with this port exposed.

Shodan also showed products such as:

- Broadcom ADSL router telnetd
- BusyBox telnetd
- Cisco router telnetd

This helped me understand why exposed services are important during reconnaissance.

An exposed service does not automatically mean that the system is vulnerable, but it gives defenders something to investigate.

---

## 🔎 Shodan Search 3 – Apache 2.4

I searched:

```text
Apache 2.4
```

Shodan showed:

**27,659 results**

The country with the most results was:

🇺🇸 **United States – 12,083**

The most common ports included:

- **80**
- **443**
- **8080**
- **8081**
- **9090**

One result contained an interesting HTTP banner:

```text
HTTP/1.1 200 OK
content-type: text/html;charset=UTF-8
content-length: 2
server: Boa/0.94.14rc20 BigIP lighttpd/1.4.28-devel-10177 MoxaHttp/1.0 Jetty(7.6.0.v20120127) Hipcam lighttpd/1.4.28-devel
```

The banner revealed several software/product identifiers, including:

- Boa
- lighttpd
- MoxaHttp
- Jetty
- Hipcam

### 💡 My Observation

> **A service can reveal useful technical information before an attacker has even authenticated.**

I also learned not to immediately call something "vulnerable" just because a version or software name appears in a banner.

**Banner information is evidence for further investigation, not automatically proof of a vulnerability.**

---

## 🛠️ Network Problem I Encountered

While trying to access Shodan, I initially experienced:

```text
ERR_QUIC_PROTOCOL_ERROR
```

I tried opening Shodan using both **Chrome** and **Edge**.

The website worked when I switched my laptop to **mobile data**.

This suggested that the problem was related to the **hostel Wi-Fi/network path rather than my laptop or browsers**.

This was also a useful troubleshooting experience because I tested the connection using another network instead of assuming that Shodan itself was unavailable.

---

# 📊 My Shodan Findings

| Requirement | My Finding |
|---|---|
| 🔢 Number of devices/results | MikroTik – **2,836,955** |
| 🌍 Country with most results | China – **425,034** |
| 🚪 Surprising open port | Port **23 (Telnet)** – **57,820 US results** |
| 📡 Specific banner/service | SNMP showing **MikroTik RouterOS x86** |
| 🖥️ Additional banner observed | Boa, lighttpd, MoxaHttp, Jetty and Hipcam |

---

# 🧠 What Changed in My Understanding

Before today, I mostly thought about cloud security as something related to companies and large data centres.

After today's work, I understand that cloud security is also directly connected to my everyday accounts.

My email, files, photos, messaging, banking, shopping, development work and other services all depend on online infrastructure.

I also understood two different perspectives:

## 🛡️ Defender Perspective

> What services do I use, who can access them, and how can I protect them?

## 🔎 Attacker Perspective

> What systems and services are exposed, and what information can I learn from them?

Shodan helped me experience the second perspective in a safe and controlled way.

---

# 🔑 Key Takeaways

## 1. ☁️ The Cloud Is Not Automatically Secure

A secure cloud provider cannot protect me from every bad configuration or weak account setting.

## 2. 🔐 MFA Is One of the Simplest Improvements I Can Make

Today's audit helped me identify missing MFA and actually enable it.

## 3. 👤 Least Privilege Matters

Giving an account or service more permissions than it needs can turn a small compromise into a much larger incident.

## 4. 🌐 Public Exposure Matters

A service does not have to be compromised to become useful to an attacker. Simply being publicly reachable can provide valuable information.

## 5. 🔎 Reconnaissance Comes Before Many Attacks

Shodan helped me see how attackers can first gather information about systems, services, ports and technologies before attempting anything further.

## 6. 🛠️ Security Work Is Not Only About Finding Vulnerabilities

Today's workflow was:

**Identify → Understand → Verify → Remediate → Document**

That is starting to feel more like real security work than simply completing a cybersecurity lesson.

---

# ⭐ My Biggest Learning From Day 17

The biggest thing I learned today is:

> **Security starts with visibility.**

I cannot protect something properly if I don't know:

- What accounts I have
- What services I use
- Who can access them
- What security controls are enabled
- What is exposed to the internet

Today's cloud audit gave me visibility into my own digital life, while Shodan showed me how visibility can also be used during reconnaissance.

The most important part was that I didn't stop at identifying problems.

> 🛡️ **I fixed the MFA issues I found.**

That made today's exercise feel much more practical and meaningful to me.

---

# 📌 Day 17 Summary

**Cloud Security + Personal Cloud Audit + Shodan Reconnaissance**

## What I Practiced

- ☁️ Understanding cloud infrastructure
- 🔐 Shared Responsibility Model
- 👤 Least privilege
- 🛡️ MFA auditing and remediation
- 📋 Mapping personal cloud services
- 🔎 Passive reconnaissance using Shodan
- 🚪 Understanding exposed ports
- 📡 Understanding service banners
- 🧠 Thinking from both defender and attacker perspectives

**Day 17 complete. 🚀**

**73 days left.**
