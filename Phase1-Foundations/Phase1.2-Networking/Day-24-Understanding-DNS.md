# 🌐 Day 24 of 90 – Understanding DNS

**Date:** August 16, 2026  
**MyFirstHack Day:** 24 of 90  
**Topic:** Domain Name System (DNS)

---

## 🎯 Objective

Today I learned about **DNS (Domain Name System)** and understood how a domain name such as `wikipedia.org` is converted into an IP address that a computer can use to connect to a website.

Before today, I knew that DNS converts a domain name into an IP address, but I didn't understand what actually happens behind that simple explanation. Today's lesson helped me understand the process, the different DNS servers involved, DNS records, and some of the security risks related to DNS.

---

## 📖 What I Learned About DNS

I understood DNS as the **phonebook of the internet**.

Humans prefer names such as `wikipedia.org`, while computers need IP addresses to communicate.

A simplified process I learned is:

**Domain name → DNS resolver → Root server → TLD server → Authoritative DNS server → IP address**

The important thing I understood is that my computer does not normally communicate directly with the authoritative DNS server. It first asks a **recursive DNS resolver**, which does the lookup work when the answer isn't already cached.

---

## ⚡ DNS Caching

DNS doesn't perform the complete lookup every time I visit a website.

My browser and operating system can have cached DNS information. The recursive resolver can also have the answer cached.

This makes DNS faster and reduces unnecessary DNS traffic.

I initially expected the DNS lookup to always involve contacting several servers, but I learned that **caching can prevent much of that work from happening again**.

---

## 🌳 The DNS Hierarchy

I learned about three important levels:

**Root servers → TLD servers → Authoritative servers**

For example, when resolving a `.com` domain:

- The **root** helps identify who handles `.com`.
- The **TLD server** identifies the authoritative servers for the domain.
- The **authoritative server** provides the actual DNS information.

I also learned that the "14-server" description in the lesson is about the different parties, caches, and infrastructure involved in a typical resolution process, rather than literally contacting 14 servers every time I open a website.

---

## 🔎 DNS Records I Practiced

I used Windows `nslookup` to investigate `wikipedia.org`.

| Record | What I learned |
|---|---|
| **A** | IPv4 address of the domain |
| **AAAA** | IPv6 address of the domain |
| **MX** | Mail servers responsible for receiving email |
| **NS** | Authoritative name servers for the domain |
| **TXT** | Additional text information, including security, verification, and email-related information |

This helped me understand that DNS is not only about finding a website's IP address. A domain's DNS records can reveal several parts of how that domain operates.

---

## 🌍 My DNS Resolver Comparison

I compared `wikipedia.org` using three DNS resolvers:

- My default DNS resolver
- Cloudflare DNS: `1.1.1.1`
- Google DNS: `8.8.8.8`

All three ultimately returned the same IPv4 address:

**103.102.166.224**

They also returned the same IPv6 address:

**2001:df2:e500:ed1a::1**

My Cloudflare query initially showed a **DNS request timeout**, but it still returned the DNS answer afterward.

This showed me that DNS requests can sometimes experience network or resolver delays even when the final answer is correct.

---

## 📧 My MX Record Finding

I used:

```text
nslookup -type=MX wikipedia.org
```

and found two mail exchangers:

- `mx-in1001.wikimedia.org`
- `mx-in2001.wikimedia.org`

Both had a preference value of **10**.

This helped me understand that a domain can have multiple mail servers instead of depending on only one server.

---

## 🏷️ My NS Record Finding

I checked the NS records and found:

- `ns0.wikimedia.org`
- `ns1.wikimedia.org`
- `ns2.wikimedia.org`

This showed me which name servers are authoritative for `wikipedia.org`.

---

## 📝 My TXT Record Finding

The TXT lookup returned several records.

One of them was:

```text
v=spf1 include:_cidrs.wikimedia.org ~all
```

I learned that this is an **SPF record**, which is related to email security and specifies which systems are allowed to send email for a domain.

I also saw domain-verification records from services such as Google and Yandex.

This helped me understand why TXT records can contain much more information than I originally expected.

---

## 🛡️ DNS Security

I learned about three major DNS attacks:

### 🔴 DNS Hijacking
An attacker changes DNS information so that a legitimate domain points to an attacker-controlled location.

### 🔴 DNS Cache Poisoning
An attacker attempts to place a fake DNS answer into a resolver's cache. Users relying on that resolver may then receive the wrong IP address until the cached information expires.

### 🔴 DNS Rebinding
An attacker uses changing DNS responses to make a browser communicate with an internal resource that should not normally be accessible from the internet.

The main thing I understood is that these attacks can result in **redirecting a user somewhere they did not intend to go**.

---

## 🔐 DNS Security Protections

### 🛡️ DNSSEC — Domain Name System Security Extensions
Helps verify that DNS responses are authentic and have not been modified.

### 🔒 DoH — DNS over HTTPS
Sends DNS queries through HTTPS, helping protect them from being easily observed or modified on the network path.

### 🔒 DoT — DNS over TLS
Protects DNS queries using TLS.

### 🛡️ HSTS — HTTP Strict Transport Security
Helps browsers enforce HTTPS connections and can prevent certain downgrade situations.

---

## 💰 MyEtherWallet Case Study

The MyEtherWallet incident helped me understand that DNS security is not just theoretical.

In the 2018 incident, attackers combined a **BGP hijack with DNS manipulation** to redirect users toward a fake website. Some users ignored a TLS certificate warning and entered their wallet credentials, which eventually resulted in stolen cryptocurrency.

The case made one thing clear:

> **A DNS attack doesn't necessarily look like a "hacking" screen. A user may simply see what appears to be the normal website while actually being sent somewhere else.**

I also learned that security is layered. DNSSEC, HSTS, HTTPS/TLS protections, and user awareness can all contribute to preventing or reducing the impact of an attack.

---

## 🤔 A Question I Had While Learning

I questioned whether a user should be blamed when an attack succeeds because they didn't notice a security warning.

I learned that cybersecurity usually isn't about simply blaming one person. Users can make mistakes, but companies also have a responsibility to build systems that reduce the chance and impact of those mistakes.

The MyEtherWallet example helped me understand that **security should work in layers instead of depending entirely on users making the perfect decision every time**.

---

## 💡 Another Important Understanding

I initially thought DNS was simply:

**Website name → IP address**

After today's work, I understand that DNS is much more than that.

It can reveal:

- where a domain points
- where its email is handled
- which DNS servers control it
- IPv4 and IPv6 information
- email-security information
- domain verification information
- other publicly available infrastructure details

This is why DNS is also important for **reconnaissance in cybersecurity**.

---

## 🧪 My Practical Work Today

Today I didn't just read about DNS. I actually used `nslookup` to investigate a real domain.

I:

1. Looked up the domain's IP addresses.
2. Compared responses from three DNS resolvers.
3. Checked the MX records.
4. Checked the NS records.
5. Checked the TXT records.
6. Checked the AAAA record.
7. Observed that the major DNS resolvers returned the same IP information.
8. Noticed that my Cloudflare DNS request initially timed out but still produced the answer.
9. Learned how different DNS record types reveal different parts of a domain's infrastructure.

---

## 😮 What Surprised Me

What surprised me most was that **one simple domain name can have so much information behind it**.

Before this task, I mostly thought of DNS as something happening automatically in the background.

Now I understand that DNS is an important part of the communication process and also an important security layer.

---

## 🧠 My Main Takeaway

> **Before a computer can connect to a website, it first needs to know where that website is. DNS provides that information, and if that information is manipulated, the user can be redirected without realizing what happened.**

I also learned that cybersecurity is not about understanding only attacks. It is equally important to understand the normal systems that attackers try to manipulate.

---

## ✅ Day 24 Status

**Day 24 completed — 66 days left. 🚀**

#MyFirstHack #Cybersecurity #DNS #Networking #CyberSecurityLearning
