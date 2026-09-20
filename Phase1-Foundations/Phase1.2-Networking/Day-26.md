# 🕵️ MyFirstHack — Day 26: Passive Reconnaissance

## 📅 Day 26 of 90

### 🎯 Topic
**Network Footprint & Passive Reconnaissance**

Day 26 was my second project in the Networks track. I used the networking knowledge from Days 21–25 to perform a real passive reconnaissance exercise.

The goal was to understand what information about a real website is already publicly available through DNS, WHOIS, Certificate Transparency, and technology profiling.

---

## 🧠 What I Learned

**Reconnaissance** is the process of collecting information about a target before deeper security work begins.

Today's five steps were:

1. 🎯 Pick a target
2. 🌐 DNS reconnaissance
3. 👤 WHOIS lookup
4. 🔐 Certificate Transparency
5. 🛠️ Technology profiling

The final output was a structured **Network Footprint Report**.

---

# 🔒 Passive Reconnaissance

### 🟢 Passive Reconnaissance

Passive reconnaissance uses information that is already publicly available, such as:

- DNS records
- WHOIS information
- Certificate Transparency logs
- Public technology information

The important point is:

> **I collect information without actively probing or attacking the target.**

### 🔴 Active Reconnaissance

Active reconnaissance directly interacts with the target.

Examples include:

- Port scanning
- Vulnerability scanning
- Aggressive crawling
- Login attempts
- Testing forms or authentication

For this project, I stayed strictly within **passive reconnaissance**.

---

# 🎯 Step 1 — Selecting a Target

I wanted to use a small clothing business because it was a manageable target for a beginner reconnaissance project.

**Target:** `newcastle.co.in`

The work was limited to:

> **Passive reconnaissance using publicly available information only.**

No port scanning, vulnerability scanning, login attempts, or other active interaction was performed.

---

# 🌐 Step 2 — DNS Reconnaissance

I used **Windows `nslookup`** to examine the target's DNS records.

I checked:

- A records
- MX records
- NS records
- TXT records

## 🔹 A Record

Command:

```text
nslookup newcastle.co.in
```

Result:

```text
newcastle.co.in → 23.227.38.65
```

### 💡 What I understood

The A record maps a domain name to an IPv4 address.

```text
newcastle.co.in
       ↓
23.227.38.65
```

---

## 📧 MX Records

Command:

```text
nslookup -type=MX newcastle.co.in
```

The domain had three mail exchangers:

```text
route1.mx.cloudflare.net
route2.mx.cloudflare.net
route3.mx.cloudflare.net
```

### 💡 What I understood

MX records tell us which mail servers handle email for a domain.

The result also showed that Cloudflare is being used for mail routing.

---

## 🌍 NS Records

Command:

```text
nslookup -type=NS newcastle.co.in
```

The authoritative name servers were:

```text
elle.ns.cloudflare.com
joel.ns.cloudflare.com
```

### 💡 What I understood

NS records tell us which name servers are authoritative for a domain.

Seeing Cloudflare name servers indicated that **Cloudflare is being used for DNS management**.

---

## 📝 TXT Record

Command:

```text
nslookup -type=TXT newcastle.co.in
```

Result:

```text
v=spf1 include:_spf.mx.cloudflare.net ~all
```

### 💡 What I understood

This is an **SPF record**. The `v=spf1` part identifies the SPF policy.

The record uses Cloudflare's mail infrastructure and ends with `~all`, which indicates a soft-fail policy for senders that do not match the listed mechanism.

---

# 🗺️ DNSDumpster Findings

I also used DNSDumpster to look at the domain's public DNS infrastructure.

One result was:

```text
www.newcastle.co.in → 23.227.38.74
```

The data associated this infrastructure with:

```text
CLOUDFLARENET
Cloudflare, Inc.
```

The hostname also showed:

```text
shops.myshopify.com
```

### 💡 My observation

This was interesting because the information suggested a combination of **Cloudflare + Shopify** rather than a simple standalone web server.

This helped me understand that the domain I see in the browser does not necessarily mean the business directly operates the underlying infrastructure.

---

# 👤 Step 3 — WHOIS Reconnaissance

I used a WHOIS lookup because I was working on Windows.

### Registrar

**Endurance International Group India Private Limited**

### Important dates

- 📅 **Created:** February 27, 2015
- 🔄 **Updated:** March 6, 2025
- ⏳ **Expires:** February 27, 2030

### Registrant

**REDACTED FOR PRIVACY**

The contact information was also privacy-protected.

### Name servers

```text
elle.ns.cloudflare.com
joel.ns.cloudflare.com
```

These matched the NS records found during DNS reconnaissance.

---

## 🧮 Domain Age

The domain was created in **2015**, making it approximately **11 years old** at the time of this analysis in 2026.

### 💡 My observation

The domain was not newly registered.

I also learned that privacy-protected WHOIS information is common and does not automatically mean a domain is suspicious.

---

# 🔐 Step 4 — Certificate Transparency

I used **crt.sh** to investigate publicly logged TLS/SSL certificates.

Initially, crt.sh showed a server/page error:

```text
Not Found
Apache Server at crt.sh Port 443
```

I retried the search and eventually obtained the certificate results.

### What I found

There were **many certificates**, so I could not reliably count the entire result set manually.

The results included:

```text
newcastle.co.in
www.newcastle.co.in
*.newcastle.co.in
```

I did not find obvious names such as `admin`, `staging`, or `dev` in the certificate results I reviewed.

### Certificate Authorities observed

- Google Trust Services
- Sectigo Limited
- Let's Encrypt

### 💡 My observation

The interesting part for me was seeing **multiple certificate authorities and repeated certificate issuance over time**.

I also learned that a wildcard certificate such as:

```text
*.newcastle.co.in
```

can cover subdomains under the domain, although it does not by itself tell us which subdomains actually exist.

---

# 🛠️ Step 5 — Technology Profiling

I used **BuiltWith** to review the technologies associated with the website.

The information I collected showed a technology stack involving:

- ☁️ Cloudflare
- 🛍️ Shopify
- Web technologies associated with the Shopify/Cloudflare setup

The DNS and technology information together suggested managed/cloud-based infrastructure rather than a simple standalone web server.

### 💡 My learning

Before this project, I mainly thought about a website like this:

```text
Domain → Website
```

After the reconnaissance, I started seeing it more like:

```text
Domain
  ↓
DNS
  ↓
Cloudflare
  ↓
Shopify / hosting infrastructure
  ↓
Web application
```

That was one of the most useful things I learned from the project.

---

# 📊 Final Reconnaissance Summary

| Area | Finding |
|---|---|
| 🎯 Target | `newcastle.co.in` |
| 🌐 A Record | `23.227.38.65` |
| 📧 MX | Cloudflare mail exchangers |
| 🌍 NS | `elle.ns.cloudflare.com`, `joel.ns.cloudflare.com` |
| 📝 TXT | SPF record using Cloudflare mail infrastructure |
| ☁️ DNS Provider | Cloudflare |
| 🛍️ Web Platform | Shopify |
| 👤 Registrar | Endurance International Group India Private Limited |
| 📅 Created | February 27, 2015 |
| ⏳ Expires | February 27, 2030 |
| 🔐 Registrant | Privacy protected |
| 📜 Certificates | Many certificates observed |
| 🏢 Certificate Authorities | Google Trust Services, Sectigo, Let's Encrypt |
| 🔎 CT names reviewed | `newcastle.co.in`, `www.newcastle.co.in`, `*.newcastle.co.in` |
| 🔒 Methodology | Passive reconnaissance only |

---

# 💡 What Surprised Me

The biggest surprise was how much information can be collected **without directly attacking or scanning a website**.

By checking DNS, WHOIS, certificate logs, and public technology information, I could build a much clearer picture of the website's infrastructure.

I also found it interesting that each source revealed a different part of the same footprint:

```text
DNS       → Where services point
WHOIS     → Domain registration information
crt.sh    → Public certificate history
BuiltWith → Technologies used by the website
```

Combining them gave me a much better understanding than relying on only one tool.

---

# 🧠 What I Learned From Doing the Project

### 1️⃣ Reconnaissance is about connecting information

One DNS record may not reveal much by itself. Combining multiple sources gives a broader picture.

### 2️⃣ Passive does not mean unimportant

This project showed me that public information alone can reveal a significant amount about an organisation's technology footprint.

### 3️⃣ Tools are only useful when I understand the output

Running `nslookup` is easy. Understanding what A, MX, NS, and TXT records mean is the more important skill.

### 4️⃣ Different sources can confirm each other

For example, the WHOIS name servers matched the NS records from DNS lookup. This helped me interpret the information more confidently.

---

# 📝 Final Takeaway

Day 26 helped me move from simply **learning networking concepts** to actually applying them.

The progression looked like:

```text
OSI Model
   ↓
IP Addresses
   ↓
Ports
   ↓
DNS
   ↓
TCP / UDP
   ↓
Reconnaissance
```

Today I used that foundation to investigate a real public website and create a structured reconnaissance report.

The biggest lesson for me was:

> **Reconnaissance is not just about collecting information. It is about connecting small pieces of publicly available information to understand the bigger picture.**

---

## 🛡️ Ethical Boundaries Followed

Throughout the project I stayed within passive reconnaissance.

- ✅ Public DNS information
- ✅ Public WHOIS information
- ✅ Public Certificate Transparency logs
- ✅ Public technology profiling
- ❌ No port scanning
- ❌ No vulnerability scanning
- ❌ No login attempts
- ❌ No form submissions
- ❌ No attempts to access internal systems

This reinforced an important professional habit:

> **If I do not have permission to actively test a system, I should stay within publicly available information.**

---

## 🎯 Project Status

- Selected a target
- Performed DNS reconnaissance
- Checked A, MX, NS and TXT records
- Used DNSDumpster
- Performed WHOIS lookup
- Checked domain age and registration information
- Investigated Certificate Transparency
- Reviewed certificate authorities and certificate names
- Performed technology profiling
- Connected findings from multiple sources
- Followed passive reconnaissance rules
- Created a reconnaissance report

**64 days left. 🚀**

#MyFirstHack #Cybersecurity #Reconnaissance #OSINT #NetworkSecurity #DNS #CyberSecurityJourney #LearningInPublic
