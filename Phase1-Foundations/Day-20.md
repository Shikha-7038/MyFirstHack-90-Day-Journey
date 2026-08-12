# 🛡️ Day 20 — Personal Threat Modeling

**📅 Date:** August 12, 2026  
**🚀 Journey:** MyFirstHack 90-Day Cybersecurity Journey  
**🎯 Topic:** Building a Personal Threat Model

---

## 📌 Overview

Today was a little different from the previous days.

Instead of learning a completely new cybersecurity concept, I used the concepts I had already learned and connected them together by creating a **personal threat model**.

The goal was to understand:

- 🔐 What I need to protect
- 👥 Who could realistically target me
- ⚔️ How an attacker might approach
- 🛡️ What defences can reduce the risk
- ⚠️ Where security gaps can exist
- 📅 Which improvements should be prioritised

I kept the detailed version of my threat model private because it contains personal security information.

This public document focuses on the **methodology and lessons I learned**.

---

# 🧠 What Is a Threat Model?

A threat model is a structured way of understanding the security risks associated with a person, system, or organisation.

It answers four basic questions:

1. 🔐 **What am I protecting?**
2. 👥 **Who might attack it?**
3. ⚔️ **How could they attack it?**
4. 🛡️ **What can I do about it?**

The main purpose is **prioritisation**.

Without a threat model, cybersecurity can become an endless checklist:

- Use MFA
- Use strong passwords
- Update software
- Use antivirus
- Review permissions
- Monitor accounts

These are useful recommendations, but not every recommendation has the same importance for every person.

A threat model helps determine **which security controls matter most for a specific situation**.

---

# 🔐 Step 1 — Asset Inventory

The first step was identifying assets that could cause meaningful damage if they were lost, stolen, exposed, or compromised.

I grouped assets into five categories:

### 👤 Account Access

Examples include:

- Primary email
- Cloud accounts
- Professional accounts
- Development/portfolio accounts
- Social-media accounts

### 💰 Financial Assets

Examples include:

- Bank accounts
- Payment services
- Investment accounts

### 📂 Data

Examples include:

- Personal documents
- Academic documents
- Photos
- Learning notes
- Coding projects

### 🌐 Reputation

Examples include:

- Professional profiles
- Portfolio
- Public projects
- Social-media presence

### 💻 Physical Access

Examples include:

- Laptop
- Smartphone
- Other personal devices

I then divided these assets into three levels:

### 🔴 Tier 1 — Critical

Assets where compromise could cause serious or long-lasting damage.

### 🟠 Tier 2 — Important

Assets where compromise would cause significant disruption but recovery would generally be possible.

### 🟢 Tier 3 — Minor

Assets that would be inconvenient to lose but could generally be recovered or replaced.

### 💡 What I Learned

The most important asset isn't necessarily the one containing the most money.

For example, an account can become highly valuable because it provides **recovery access to other accounts**.

This made me start thinking about security in terms of **connections between assets**, rather than looking at every account separately.

---

# 👥 Step 2 — Threat Actor Profile

The next step was identifying who might realistically attack.

I learned that "hackers" should not be treated as one single group.

### 🟢 Tier A — Opportunistic Mass Attackers

These attackers use automated or large-scale techniques such as:

- Generic phishing
- Credential stuffing
- Malicious links
- Automated scams

Almost every internet user can encounter these threats.

### 🟠 Tier B — Opportunistic Targeted Criminals

These attackers may become more interested in a particular person after discovering that the person has something valuable.

Examples include:

- Account takeover
- Targeted phishing
- Financial fraud
- Social engineering

### 🔴 Tier C — Targeted Criminals

These attackers specifically select a person for personal or financial reasons.

### 🟣 Tier D — Investigative or Activist Actors

These may include investigators, activists, or other actors conducting targeted OSINT.

### ⚫ Tier E — State Actors

These are highly capable actors with resources for sophisticated operations.

### 💡 What I Learned

A good threat model should **not exaggerate the threat**.

It is important to identify the highest realistic threat level rather than assuming that every person needs protection against the most sophisticated attackers.

This prevents wasting time and resources on threats that are extremely unlikely while ignoring more realistic ones.

---

# ⚔️ Step 3 — Attack Scenarios

The next step was to create realistic attack scenarios.

Instead of creating three identical phishing examples, I looked at different attack paths.

## 📧 Scenario 1 — Social Engineering

A professional-looking message can be created around a person's interests, education, career, or online activity.

The attacker could:

1. 🔎 Gather public information.
2. 🎯 Identify something that would interest the target.
3. ✉️ Create a convincing message.
4. 🔗 Deliver a malicious link or request.
5. 🧠 Depend on the target taking an unsafe action.
6. 🔓 Attempt to obtain account access.
7. 💰 Use the access for financial, data, or reputational gain.

### Lesson

**Social engineering attacks the person, not just the technology.**

---

## 💳 Scenario 2 — Fake Financial Alert

A common social-engineering technique is creating a sense of urgency.

For example, an attacker could claim that an unexpected transaction has occurred.

The intended reaction might be:

> "Something is wrong. I need to act immediately."

The attacker then tries to direct the victim toward a malicious link, fake support number, or fraudulent request.

### Lesson

A useful defence is to **verify information through an independent trusted channel**.

For example:

**Don't use the link in the message → open the official application yourself → verify the information.**

---

## 📱 Scenario 3 — Malicious Application

Attackers can also use a person's interests to make malicious software appear legitimate.

For example, someone interested in cybersecurity or education might receive a message about:

- A study tool
- A cybersecurity application
- A training resource
- A professional opportunity

The attacker could attempt to convince the target to install software from an untrusted source.

### Lesson

The source of software matters.

Using trusted application stores and avoiding unexpected application downloads can reduce this type of risk.

---

# 🛡️ Step 4 — Defence Mapping

After creating attack scenarios, I looked at the different stages of an attack and asked:

**What defence could stop the attacker here?**

This is where I learned the difference between a **defence** and a **gap**.

### Example

**Attack:** Phishing

**Defence:**
- Spam filtering
- MFA
- Password manager
- Security awareness
- Login alerts

**Possible gaps:**
- User clicks the malicious link
- User provides information voluntarily
- Old connected applications remain authorised
- Recovery methods are not reviewed

This showed me that having one strong security control does not automatically secure the entire attack chain.

Security needs **multiple layers**.

---

# 🔍 Defence-in-Depth

One of the important lessons from today's exercise was the idea of **defence in depth**.

Instead of depending on one security control, several controls can work together.

For example:

**Strong password → MFA → Login alerts → Secure recovery → Application review**

If one layer fails, another layer can still provide protection.

This is why cybersecurity should be viewed as a system rather than a single setting.

---

# 📊 Step 5 — Priority Matrix

After identifying potential gaps, I learned that not every gap deserves the same amount of attention.

A simple priority matrix can compare:

- **Likelihood** — How likely is the threat?
- **Impact** — How serious would the result be?

### 🔴 High Likelihood + High Impact

**Do first**

These are the most important risks.

### 🟠 High Likelihood + Low Impact

**Quick fixes**

These may not cause major damage individually but are worth addressing.

### 🟡 Low Likelihood + High Impact

**Plan for later**

These deserve attention but may not be the immediate priority.

### 🟢 Low Likelihood + Low Impact

**Defer**

These should not consume significant effort while more important risks remain.

---

# 📅 90-Day Security Planning

The final part was converting the analysis into actions.

Instead of creating a huge list of improvements, I learned to select a **small number of realistic priorities**.

A good security action should include:

### 🎯 Action

What exactly will be changed?

### 📅 Deadline

When will it be completed?

### ✅ Verification

How will I prove that it was actually completed?

This makes the plan measurable rather than just a list of intentions.

---

# 💡 What I Learned Today

### 1️⃣ Cybersecurity is about prioritisation

I don't need to defend against every possible attack equally.

I need to understand which threats are realistic and which assets matter most.

### 2️⃣ An account can be valuable because of its connections

An account may not contain money itself but could provide access to other important accounts through recovery mechanisms.

### 3️⃣ MFA is important, but it isn't the entire defence

MFA protects authentication, but other areas such as recovery methods, connected applications, permissions, and user behaviour also matter.

### 4️⃣ Human behaviour is part of cybersecurity

Opening an official application directly instead of following a suspicious link can prevent an attack.

### 5️⃣ Don't assume a security control exists

If I don't know whether a security feature exists, I should verify it rather than assume.

### 6️⃣ Threat modelling is different from a checklist

A checklist gives general advice.

A threat model helps answer:

> **Which advice matters most for this particular person?**

---

# 📝 Personal Reflection

Today's exercise connected many topics I had learned during the first part of my cybersecurity journey.

Earlier, I was learning concepts individually:

**IP addresses → DNS → HTTP/HTTPS → phishing → social engineering → Cyber Kill Chain**

Today I used those concepts together to think like a security analyst.

The biggest change in my thinking was understanding that cybersecurity is not only about finding vulnerabilities.

It is also about:

**Identify → Analyse → Prioritise → Defend → Improve**

A security professional needs to know what matters most before deciding what to protect first.

---

# 🛡️ Why I Kept the Detailed Threat Model Private

The full threat model contains personal security information.

Publishing details about:

- Specific important accounts
- Recovery methods
- Financial security
- Personal attack scenarios
- Security gaps
- Device dependencies

could provide unnecessary reconnaissance information to someone who wanted to target me.

Therefore, I kept the **full personal threat model private** and created this public version to document the methodology and learning instead.

This was itself an important cybersecurity lesson:

> **Good security documentation also requires knowing what information should not be made public.**

---

# 🎯 Final Takeaway

Day 20 taught me how to move from **learning cybersecurity concepts to applying them**.

I now understand how to:

🔐 Identify assets  
👥 Profile realistic threat actors  
⚔️ Build attack scenarios  
🛡️ Map defences and gaps  
📊 Prioritise risks  
📅 Create measurable security actions

The most important lesson was simple:

**Security is not about protecting everything equally. It is about protecting what matters most from the threats that are most realistic.**

---

## ✅ Day 20 Completed

**Project:** Personal Threat Model  
**Focus:** Risk analysis and security prioritisation  
**Status:** Completed

🔒 **Full personal threat model:** Kept private  
🌐 **Public documentation:** Sanitised for portfolio use

**Next:** 🌐 Networks Track — understanding how data moves between machines.