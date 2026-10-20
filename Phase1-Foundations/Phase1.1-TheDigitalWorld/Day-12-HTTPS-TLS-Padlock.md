# 🔐 Day 12 – HTTPS, TLS & Understanding the Trust Behind the Padlock

**📅 Date:** August 04, 2026

---

# 🎯 Objective

The objective of today's lesson was to understand how **HTTPS** protects communication on the web, how **TLS encryption** works, what the browser's **padlock icon** actually means, and why it should never be treated as proof that a website is safe.

I also learned how **digital certificates** are issued, the role of **Certificate Authorities (CAs)**, how trust is established between browsers and websites, and why security analysts inspect much more than just the presence of HTTPS when evaluating a website.

Unlike what I believed before, today's lesson showed that:

> **HTTPS secures the communication channel, not the trustworthiness of the website itself.**

---

# 📖 Introduction

For years, I have seen the small **padlock icon** in my browser and assumed it meant a website was completely safe.

Today's lesson completely changed that understanding.

I discovered that the padlock **does not guarantee** a website is genuine or trustworthy. Instead, it only confirms that the communication between my browser and that website is encrypted.

This was one of the biggest mindset shifts so far because I realized that **phishing websites can also use HTTPS and display the same trusted padlock icon.**

---

# 📚 What I Learned

## 🌐 1. HTTP vs HTTPS

The lesson began by explaining the difference between HTTP and HTTPS.

### 📄 HTTP

HTTP sends information across the internet in **plain text**.

If someone intercepts the network traffic, they can read everything being transmitted, including:

- 👤 Usernames
- 🔑 Passwords
- 💳 Credit card numbers
- 📝 Personal information

The lesson compared HTTP to sending a **postcard through the mail**, where anyone handling it can read its contents.

---

### 🔒 HTTPS

HTTPS protects communication by encrypting the data before it leaves my browser.

Instead of readable text, anyone intercepting the traffic only sees encrypted information that appears as random characters.

Only two parties can decrypt that information:

- 💻 My browser
- 🌍 The destination website's server

This protects the confidentiality of data while it travels across the internet.

---

## 💡 My Learning

One question immediately came to my mind:

> **If a website is fake but uses HTTPS, can it still read my information?**

Initially, I assumed encryption would prevent this.

After exploring the concept, I learned that HTTPS only encrypts the connection **between my browser and the website I choose to visit.**

If I accidentally visit a phishing website with HTTPS and enter my password, the fake website can still decrypt and read my information because **it is the intended recipient of the encrypted connection.**

This helped me understand an important cybersecurity principle:

> **HTTPS protects the journey of the data, not whether the destination deserves to receive it.**

---

# 🌍 2. Why HTTP Became HTTPS

The lesson explained why the internet gradually moved away from HTTP.

One of the biggest turning points was the **Firesheep** attack.

Attackers connected to public Wi-Fi networks and captured users' session cookies because many websites were still using HTTP.

Since cookies travelled in plain text, attackers could hijack active user sessions without needing passwords.

As a result:

- 🌐 Most websites now automatically redirect users to HTTPS.
- ⚠️ Browsers mark HTTP websites as **Not Secure**.
- 🔍 Search engines prioritize HTTPS websites.
- 🆓 Free certificates from **Let's Encrypt** made HTTPS accessible to everyone.

Today, around **95% of web traffic uses HTTPS.**

---

# 🔐 3. What the Padlock Actually Proves

Before today, I believed the browser's padlock meant a website was trustworthy.

I learned that this assumption is incorrect.

The padlock only confirms three things:

1. 🔒 My browser and the server established an encrypted connection.
2. 📜 The server presented a valid digital certificate.
3. ✅ A trusted Certificate Authority (CA) verified that certificate.

### ❌ The Padlock Does NOT Prove

- The website is legitimate.
- The company is trustworthy.
- The website is free from malware.
- The website is the one I intended to visit.

---

## 💭 My Reflection

This completely changed how I interpret the padlock icon.

Instead of treating it as proof that a website is safe, I now see it as **only the beginning of the verification process.**

---

# 🏢 4. Certificate Authorities (CAs)

I learned that browsers trust around **100–200 Root Certificate Authorities** around the world.

These organizations verify website ownership and issue digital certificates.

Some common CAs include:

- GlobalSign
- DigiCert
- Sectigo
- Let's Encrypt
- Google Trust Services

Every browser contains a built-in list of trusted CAs.

Whenever I visit an HTTPS website, my browser checks whether the certificate has been signed by one of these trusted authorities.

---

# ⚠️ The DigiNotar Incident

One of the most interesting parts of today's lesson was learning about the **DigiNotar breach (2011).**

Attackers compromised the Dutch Certificate Authority DigiNotar and created hundreds of fraudulent certificates for major websites, including Google.

Because the certificates appeared valid, browsers trusted them.

The attackers used these fake certificates to monitor approximately **300,000 Gmail users** in Iran.

Although users saw the familiar HTTPS padlock, their communications were being intercepted.

---

## 💡 My Learning

This incident helped me understand that the internet's trust model depends heavily on Certificate Authorities.

If even one trusted CA is compromised, attackers can misuse that trust.

It also explained why browsers regularly remove compromised Certificate Authorities from their trusted lists.

---

# 🔎 5. Reading URLs Like a Security Analyst

Today's lesson introduced a habit used by security professionals.

Instead of focusing only on the padlock or company logo, analysts carefully examine:

- 🌐 The full domain name
- 📜 Certificate issuer
- 📅 Certificate validity dates
- 🔗 Complete URL structure
- ⚠️ Look-alike domains

### Example

```
paypal.com.security-update.net
```

Although it begins with **paypal.com**, the real domain owner is:

```
security-update.net
```

Reading URLs **from right to left** helps identify phishing websites that imitate legitimate brands.

---

# 🛡️ 6. HTTPS Is Not the Final Layer of Security

Another important lesson was understanding what HTTPS **cannot** protect.

Even if HTTPS is working perfectly:

- ⚠️ Malicious JavaScript running inside a webpage can steal information before encryption occurs.
- 🎣 A phishing website can still receive and decrypt any information I willingly submit.
- 💾 Poor server security can still expose stored customer data.

---

## 💡 My Understanding

One example that helped me understand this involved an online shopping website.

If malicious JavaScript is injected into the checkout page, it can secretly read:

- 💳 Credit card details
- 🔑 Passwords
- 🏠 Addresses

before HTTPS encrypts the data.

This showed me that HTTPS protects data **while travelling across the network**, but it **cannot stop malicious code already running inside the webpage itself.**

---

# 🧪 Practical Task 1 – Inspecting a Real Certificate

I inspected the HTTPS certificate for **www.bbc.com**.

### 📌 Findings

| Field | Result |
|--------|---------|
| 🌐 Website | www.bbc.com |
| 👤 Issued To | BRITISH BROADCASTING CORPORATION |
| 🏢 Issued By | GlobalSign RSA OV SSL CA 2018 |
| 📅 Issued On | 9 July 2026 |
| ⏳ Expires On | 24 January 2027 |
| 📆 Validity | Approximately **199 days** |

### 💡 My Observation

I was surprised to see how much technical information is stored inside a certificate.

Besides the website name, I found:

- Organization name
- Certificate Authority
- Validity period
- Certificate fingerprint
- Public key

This helped me understand how browsers verify a website's identity before establishing an encrypted connection.

---

# 🧪 Practical Task 2 – Viewing an HTTP Website

I visited **NeverSSL.com**, one of the few websites that intentionally uses HTTP.

### 📌 Findings

- ⚠️ Browser displayed **Not Secure**.
- 🔓 No TLS information was available because no encrypted connection was established.

### 💡 My Learning

At first, I thought I should see TLS information on every website.

After investigating further, I learned that TLS only exists when a website uses HTTPS.

Since NeverSSL intentionally avoids HTTPS, there is **no TLS handshake** to display.

---

# 🧪 Practical Task 3 – Testing HTTPS with SSL Labs

I tested **github.com** using the **Qualys SSL Labs** analyzer.

### 📌 Results

| Item | Result |
|------|--------|
| 🌐 Website | github.com |
| 🏆 Grade | **A+** |
| 🔒 TLS Version | TLS 1.3 |

### 💭 My Opinion

I would trust GitHub with sensitive information because it achieved an **A+** rating and showed no major security warnings.

This practical exercise showed me how security analysts evaluate HTTPS configurations instead of simply assuming a website is secure.

---

# ⚡ Challenges I Faced

During today's lesson, I encountered several questions that deepened my understanding:

- 🤔 I initially believed the browser padlock meant a website was completely safe.
- 🤔 I wondered whether a fake HTTPS website could still decrypt information.
- 🤔 I expected HTTPS alone to protect users from phishing attacks.
- 🤔 I was confused when I couldn't find TLS information on NeverSSL.
- 🤔 I wanted to understand why malicious JavaScript can still steal information even when HTTPS is enabled.

Researching these questions helped me understand **not only how HTTPS works, but also where its protection ends.**

---

# 🛠️ Skills Developed

- 🌐 Understanding HTTP and HTTPS
- 🔒 Learning how TLS encrypts communication
- 📜 Inspecting digital certificates
- 🏢 Understanding Certificate Authorities
- 🔍 Reading URLs like a security analyst
- 🛡️ Identifying the limitations of HTTPS
- 📊 Evaluating website certificates
- 🧪 Using SSL Labs to assess HTTPS security
- 💭 Developing a security-focused mindset

---

# 🎯 Key Takeaways

- HTTPS encrypts communication but **does not guarantee** a website is safe.
- The browser padlock only confirms **encryption, identity verification, and certificate validation**.
- Certificate Authorities are responsible for establishing trust on the internet.
- A compromised CA can undermine that trust, as shown by the DigiNotar incident.
- Phishing websites can use valid HTTPS certificates.
- Malicious JavaScript can steal data **before HTTPS encrypts it**.
- Security analysts inspect **domains, certificates, and URLs**, not just the padlock.
- Tools like **Certificate Viewer** and **SSL Labs** help evaluate website security.

---

# 📝 Conclusion

Day 12 completely changed my understanding of one of the most familiar symbols on the internet—the browser's **padlock icon**.

Instead of seeing it as proof that a website is trustworthy, I now understand that it simply indicates an **encrypted connection** between my browser and the destination website.

The practical exercises of inspecting certificates, exploring an HTTP website, and evaluating GitHub's HTTPS configuration helped reinforce these concepts beyond theory.

More importantly, today's lesson taught me that cybersecurity is not about trusting symbols—it is about understanding **what those symbols actually guarantee and where their protection ends.**