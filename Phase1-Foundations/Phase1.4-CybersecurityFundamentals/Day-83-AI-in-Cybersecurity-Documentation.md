# Day 83 — How Attackers Use AI in Cybersecurity

## Overview

Day 83 explores how attackers use artificial intelligence (AI) to amplify familiar cyberattack methods. AI can make certain attacks more convincing, faster, easier to scale, and accessible to people with less experience. It does not make cybersecurity fundamentals obsolete.

## 1. AI as a Force Multiplier

AI is best understood as a **force multiplier**: it can strengthen existing techniques rather than necessarily creating entirely new categories of attack.

Familiar threats such as phishing, social engineering, reconnaissance, impersonation, and attempts to exploit vulnerabilities still matter. AI can change the speed, quality, scale, or accessibility of these activities.

## 2. Making Attacks More Convincing

### AI-assisted phishing

Traditional phishing messages sometimes contained warning signs such as poor grammar, awkward phrasing, generic greetings, and unnatural wording. AI can produce fluent, natural-sounding messages, making bad writing a less reliable warning sign.

A polished message is not proof that the sender is legitimate. Poor grammar can still be suspicious, but good grammar cannot establish trust.

### Personalised spear-phishing

Spear-phishing targets a particular person or organisation. AI can help turn gathered information into tailored messages more quickly and at greater scale.

For example, information about someone's professional interests might be used to make a fraudulent opportunity seem relevant. This connects to Day 82, which covered OSINT and how publicly available details can be combined.

### Impersonation and deepfakes

AI can generate or manipulate images, audio, and video. These synthetic media can be misused to imitate a person or lend false credibility to a request.

Examples include fake audio that imitates an executive's voice or manipulated video used to support a scam. The underlying technique remains impersonation or social engineering; AI can make it more convincing.

## 3. Making Attacks Faster, Bigger, and More Accessible

### Faster reconnaissance

AI can help gather, organise, analyse, and summarise large amounts of publicly available information. This may speed up reconnaissance and help attackers research multiple targets with less manual effort.

This connects to OSINT (Day 82) and the reconnaissance stage of the Cyber Kill Chain.

### Greater scale

AI can help generate variations of messages, create content, or assist with certain coding tasks. Automation and generation can allow attackers to make more attempts in less time and at a lower cost.

The threat may grow even when the underlying attack method remains the same: more attempts can reach more targets.

### Lower barrier to entry

AI assistance can help less-experienced attackers attempt certain tasks that once required more knowledge or effort. This connects to the discussion of script kiddies and threat actors on Day 74.

AI does not automatically turn a novice into an expert. Its output can be wrong, and sophisticated attacks can still require substantial expertise and resources.

## 4. The Measured Reality

AI-assisted attacks are a genuine concern, especially when it comes to convincing phishing, social engineering, impersonation, speed, and scale. They should not be dismissed as hype.

At the same time, AI does not make defence hopeless. Many AI-assisted attacks are still familiar attack types, so established defensive principles remain valuable.

### Defensive practices that still matter

- **Verify requests independently:** Use a separate, trusted channel to confirm unusual or sensitive requests.
- **Be cautious of urgency:** Pressure to act immediately, disclose credentials, or transfer money deserves scrutiny.
- **Handle unexpected links and attachments carefully:** Do not rely on a message's polished appearance.
- **Use multi-factor authentication (MFA):** MFA adds a layer of protection if a password is compromised, though it does not stop every account attack.
- **Patch and update systems:** Fixing known vulnerabilities reduces opportunities for exploitation.
- **Harden systems:** Reduce unnecessary services, access, and insecure configurations.
- **Use defence in depth:** Multiple complementary controls reduce reliance on a single defence.

The key adaptation is to rely less on superficial signals—such as grammar or a familiar-sounding voice—and more on verification, context, and layered controls.

## 5. Day 83 Task — Reason About AI-Amplified Attacks

### Step 1: State the core framing

AI does not necessarily create fundamentally new types of cyberattacks; it amplifies familiar attacks by making them more convincing, faster, more scalable, and accessible to more people. Existing security knowledge remains relevant because understanding phishing, reconnaissance, vulnerabilities, and defence in depth provides a foundation for recognising and defending against AI-assisted versions of these threats.

### Step 2: Map AI to familiar attacks

- **Phishing:** AI can generate fluent, personalised messages quickly, making phishing harder to identify through grammar alone.
- **Reconnaissance / OSINT:** AI can rapidly organise, analyse, and summarise public information to help attackers research targets.
- **Impersonation / social engineering:** AI-generated or manipulated voices, images, and videos can make impersonation attempts more realistic.
- **Lower skill barrier:** AI can help less-experienced attackers attempt certain tasks, although it does not make them experts.

### Step 3: Reason about the weakened tell

Bad grammar and awkward writing were traditional phishing warning signs. AI can generate polished messages, so the absence of writing mistakes is no longer reliable proof that a message is genuine.

Instead, verify suspicious requests through trusted channels, be cautious of urgency and unusual requests, avoid unexpected links and attachments, and use MFA to strengthen account security. Assess the sender, context, and requested action—not just how professional the message looks or sounds.

### Step 4: Does AI make defence hopeless?

No. AI genuinely strengthens certain attacks by making them more convincing, faster, more scalable, and accessible. Defenders must adapt because traditional clues such as poor grammar may be less useful. However, AI amplifies many familiar attack methods, and proven practices—independent verification, MFA, patching, hardening, and defence in depth—remain important. The appropriate response is to take AI seriously while strengthening established security practices, not to assume defence is impossible.

### Step 5: Apply it to myself

My Day 82 OSINT exercise showed how publicly available information can be combined to build a picture of a person. An attacker could potentially use AI to turn professional interests or learning-related details into a polished, personalised phishing message—for example, a fraudulent cybersecurity internship opportunity.

Relevant details and professional writing would not prove the sender or opportunity was genuine. I would independently check the sender and opportunity, verify unusual requests through an established trusted channel, avoid unexpected links or attachments, and be cautious of pressure to provide credentials, disclose sensitive information, or make a payment. I would continue using MFA to add protection to my accounts.

This approach relies on verification and judgement rather than spotting bad grammar. It does not imply that I have been personally targeted.

## 6. Key Takeaways

- AI is a **force multiplier** for familiar cyber threats, not a reason to assume all attacks are entirely new.
- AI can make phishing more fluent and personalised, reconnaissance faster, impersonation more realistic, and attacks easier to scale.
- AI can lower the barrier to attempting some tasks, but it does not make every user an expert.
- Poor grammar is a weaker standalone phishing signal; polished writing does not prove legitimacy.
- Independent verification, caution around urgency, MFA, patching, system hardening, and defence in depth remain valuable.
- A realistic security mindset neither dismisses AI nor treats defence as hopeless.
- Existing cybersecurity fundamentals are the foundation for responding to AI-amplified threats.

## Connection to Day 84

Day 83 focuses on how attackers use AI. Day 84 will explore the other side: how defenders and security operations teams can use AI to support detection, analysis, and response. Understanding both sides provides a more complete picture of AI in cybersecurity.
