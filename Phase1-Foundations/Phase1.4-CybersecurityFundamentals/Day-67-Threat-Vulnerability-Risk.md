# Day 67 — Threat, Vulnerability, and Risk

## Topic

**Threat, Vulnerability, and Risk**

---

## 1. Threat

A **threat** is anything that could potentially cause harm to a system, organization, or person.

Examples of threats include:

- Attackers
- Ransomware groups
- Nation-state attackers
- Fire
- Floods
- Hardware failure
- Power outages
- Careless employees

A threat generally exists independently of your system and is largely outside your direct control.

---

## 2. Vulnerability

A **vulnerability** is a weakness that a threat could exploit.

Examples include:

- Unpatched software
- Weak passwords
- Unnecessary open ports
- Misconfigured permissions
- Untrained employees
- Lack of appropriate security controls

Vulnerabilities are generally within an organization's control and can often be reduced or removed through security controls and hardening.

### Threat vs. Vulnerability

**Threat = Something that could cause harm**

**Vulnerability = A weakness that could be exploited**

A threat by itself does not necessarily cause harm, and a vulnerability by itself does not necessarily cause harm. Harm becomes possible when a threat can exploit a vulnerability.

### Relationship

**Threat + Vulnerability → Potential Harm**

---

## 3. Risk

**Risk** is the potential for loss or harm when a threat can exploit a vulnerability, considering the likelihood and impact of the event.

### Likelihood

**Likelihood** is how probable it is that the harmful event will occur.

Factors that can affect likelihood include:

- How exposed the system is
- Whether the vulnerability is known
- Whether attackers are actively targeting it
- The capability of potential attackers
- The motivation of potential attackers

### Impact

**Impact** is how much damage could occur if the event happens.

Impact can involve:

- Confidentiality
- Integrity
- Availability
- Financial loss
- Operational disruption
- Reputation
- Safety

### Risk Relationship

**Likelihood + Impact → Risk**

Risk can be high when an event is both likely to happen and capable of causing significant damage.

---

## 4. Same Vulnerability, Different Risk

A vulnerability does not automatically create the same level of risk in every environment.

Risk depends on the context, especially the likelihood of exploitation and the potential impact.

For example, a weak password on a critical system containing important customer information could create significant risk. The same type of weakness on an isolated test system containing no important information could create much less risk.

This means security teams should consider:

- How likely is the vulnerability to be exploited?
- What could happen if it is exploited?
- How important is the affected system or information?

---

## 5. Risk Responses

After identifying and evaluating a risk, an organization can choose how to respond.

There are four fundamental risk responses.

### 1. Reduce

**Reduce** the risk by lowering the likelihood or impact.

Examples:

- Patch vulnerable software
- Harden systems
- Add security controls
- Improve access controls
- Add monitoring

### 2. Accept

**Accept** the risk when an organization consciously decides that the risk is small enough to live with.

Accepting risk does not mean ignoring it. The risk is identified, considered, and deliberately accepted.

Sometimes the cost of eliminating a small risk can be greater than the potential harm.

### 3. Transfer

**Transfer** means shifting some of the consequences of a risk to another party.

Example:

- Cyber insurance

Risk transfer does not necessarily eliminate the underlying threat or vulnerability. It can instead shift some of the financial consequences to another party.

### 4. Avoid

**Avoid** the risk by eliminating the activity that creates it.

For example, an organization may decide not to introduce a feature that creates unnecessary security exposure when the feature is not needed.

---

## 6. Risk-Based Security Decisions

Cybersecurity is not about eliminating every possible risk.

Organizations have limited:

- Time
- Money
- People
- Resources

Security teams therefore need to evaluate risks and make deliberate decisions about how each risk should be handled.

### Overall Framework

**Threat + Vulnerability**

↓

**Potential Harm**

↓

**Likelihood + Impact**

↓

**Risk**

↓

**Reduce / Accept / Transfer / Avoid**

---

# Day 67 Tasks

## Task 1 — Define Threat, Vulnerability, and Risk

### Threat

A threat is something that could potentially cause harm to a system, organization, or person.

### Vulnerability

A vulnerability is a weakness that a threat could exploit.

### Risk

Risk is the potential for loss or harm when a threat can exploit a vulnerability, considering likelihood and impact.

### Relationship

A threat and a vulnerability can combine to create the possibility of harm. Likelihood and impact help determine the resulting level of risk.

**Threat + Vulnerability → Potential Harm → Likelihood + Impact → Risk**

---

## Task 2 — Classify the Following

| Item | Classification | Reason |
|---|---|---|
| Unpatched software | Vulnerability | It is a weakness that can be exploited. |
| Ransomware gang | Threat | It is a potential source of harm. |
| Weak password | Vulnerability | It creates a weakness that can be exploited. |
| Flood | Threat | It can cause physical or operational damage. |
| Employee untrained to spot phishing | Vulnerability | The lack of training creates a weakness that phishing threats can exploit. |
| Nation-state attacker | Threat | It is a potential source of deliberate harm. |

---

## Task 3 — Compare Risk

Consider two systems with a weak password and a threat capable of exploiting it.

The system containing a **critical customer database and an administrative account** represents the higher-risk situation because successful exploitation could have a much greater impact on important information and operations.

An **isolated test system with a throwaway account** would generally have lower impact, assuming it contains no important information and has limited connectivity.

The important point is that the same type of vulnerability can create different levels of risk depending on its context, likelihood, and impact.

---

## Task 4 — Choose the Appropriate Risk Response

### Scenario 1: Critical unpatched server facing active attacks

**Response: Reduce**

The risk should be reduced by addressing the vulnerability, such as patching the server and adding appropriate security controls.

### Scenario 2: Tiny, very unlikely risk that costs a fortune to eliminate

**Response: Accept**

The organization can consciously accept the risk when the potential harm is very small compared with the cost of eliminating it.

### Scenario 3: Financial impact of a possible breach that the company cannot fully prevent

**Response: Transfer**

Some of the financial consequences can be transferred through mechanisms such as cyber insurance.

### Scenario 4: Risky new feature that the business does not need

**Response: Avoid**

The organization can avoid the risk by deciding not to introduce the unnecessary feature.

---

## Task 5 — Apply the Concepts to Personal Digital Security

A personal example can be a private online account.

### Threat

An attacker attempting to gain unauthorized access.

### Vulnerability

A reused or weak password, lack of multi-factor authentication, or an insecure account-recovery method.

### Risk

An attacker could gain access to private information, take control of the account, or potentially use the account to access or reset other accounts.

### Response

**Reduce** the risk by:

- Using a unique, strong password
- Enabling multi-factor authentication
- Monitoring account activity and login alerts
- Keeping account-recovery options secure

---

# Key Takeaways

- A **threat** is something that could cause harm.
- A **vulnerability** is a weakness that a threat could exploit.
- Harm becomes possible when a **threat meets a vulnerability**.
- **Risk** considers the potential harm, likelihood, and impact.
- The same vulnerability can create different levels of risk depending on the environment and consequences.
- Risk can affect **confidentiality, integrity, availability, finances, operations, reputation, and safety**.
- The four fundamental risk responses are **Reduce, Accept, Transfer, and Avoid**.
- Accepting a risk is a deliberate decision, not the same as ignoring it.
- Good security decisions focus on **managing risk**, not eliminating every possible risk.

### Day 67 Framework

> **Threat → Vulnerability → Likelihood + Impact → Risk → Response**
