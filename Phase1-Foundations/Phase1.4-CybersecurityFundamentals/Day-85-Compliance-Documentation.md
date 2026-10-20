# Day 85 — Map the Compliance Landscape

**Journey:** MyFirstHack 90-Day Journey  
**Topic:** Compliance in cybersecurity  
**Task type:** Thinking and writing — no terminal commands

## Learning objectives

- Define compliance and explain why it exists.
- Recognise four major categories of regulation and standards.
- Match compliance categories to different types of organisations.
- Explain why compliance and security are related but not identical.
- Understand how compliance influences cybersecurity work and careers.

---

## Notes: What is compliance?

**Compliance** means meeting the laws, regulations, standards, and other applicable requirements an organisation must follow—and being able to demonstrate that those requirements are met.

Requirements depend on an organisation's activities, location, industry, and the types of data it handles.

### Why compliance exists

1. **Protecting people:** Requirements help protect personal information, medical records, financial data, and privacy from misuse or unauthorised access.
2. **Setting a baseline:** Compliance establishes minimum requirements that organisations must meet to maintain a basic level of protection.
3. **Accountability and trust:** Documentation, evidence, and audits help demonstrate that requirements are being met and make organisations answerable for their responsibilities.

## The four main categories

| Category | What it covers | Example |
|---|---|---|
| Personal-data privacy laws | Rules for processing and protecting personal information and respecting privacy rights | **GDPR** — General Data Protection Regulation |
| Sector-specific regulations | Requirements for particular sectors or activities, such as healthcare or corporate financial reporting | **HIPAA** — certain US health-information protections; **SOX** — US corporate financial reporting and internal controls |
| Payment-card industry standards | Security requirements for protecting payment-card data | **PCI DSS** — Payment Card Industry Data Security Standard |
| Security frameworks and standards | Structured requirements or guidance for managing information security | **ISO/IEC 27001** — requirements for an Information Security Management System (ISMS) |

### Important distinctions

- **GDPR** is a privacy regulation; its application depends on the relevant processing and circumstances.
- **HIPAA** is a US law that protects certain health information for covered entities and business associates.
- **SOX** focuses on corporate financial reporting and internal controls for relevant companies; it is not a general rule for all customer financial records at every bank.
- **PCI DSS** is an industry standard that may be required through payment-card arrangements and contracts.
- **ISO/IEC 27001** is an international standard for an ISMS. Organisations may adopt it voluntarily or need to meet it because of contractual or other applicable requirements.

The aim is to recognise what each category covers, rather than memorise every regulation.

---

## Task: Map the compliance landscape

### Step 1 — Define compliance and why it exists

**Definition:**  
Compliance means following the laws, regulations, standards, and other applicable requirements an organisation must meet, and being able to demonstrate that it meets them.

**Three reasons compliance exists:**

- **Protecting people:** It helps safeguard personal information, medical records, financial data, and privacy.
- **Setting a baseline:** It establishes minimum security and privacy requirements organisations must meet.
- **Accountability and trust:** Records, evidence, and audits help verify that requirements are met and hold organisations accountable.

### Step 2 — Sort the categories

1. **Personal-data privacy laws — GDPR:** Govern the handling and protection of personal information and establish privacy rights.
2. **Sector-specific regulations — HIPAA / SOX:** Apply requirements to particular areas, such as certain US health information under HIPAA and corporate financial reporting/internal controls under SOX.
3. **Payment-card standards — PCI DSS:** Set security requirements for protecting payment-card data.
4. **Security frameworks and standards — ISO/IEC 27001:** Provide requirements for establishing and improving an Information Security Management System.

### Step 3 — Match organisations to their rules

#### 1. Hospital storing patient records

- **Sector-specific regulation:** HIPAA may apply to covered US healthcare entities and their business associates.
- **Privacy laws:** Applicable laws may govern patient personal and medical information.
- **Security standards:** ISO/IEC 27001 may help manage information-security risks.

**Reason:** Hospitals handle sensitive health information that needs appropriate protection against unauthorised access, loss, or misuse.

#### 2. Online shop taking credit-card payments

- **Payment-card standard:** PCI DSS applies when payment-card data is stored, processed, or transmitted, subject to its scope.
- **Privacy laws:** Applicable privacy laws may govern customer names, addresses, contact details, and other personal information.
- **Security standards:** ISO/IEC 27001 may support information-security management.

**Reason:** The shop must protect payment-card data and customers' personal information.

#### 3. Social media company holding millions of users' personal data

- **Privacy laws:** GDPR may apply depending on the company's activities and the people whose data it processes.
- **Security standards:** ISO/IEC 27001 may help manage information-security risks.
- **Other rules:** Additional requirements may apply based on location and activities.

**Reason:** The company processes large amounts of personal information, so privacy and data protection are important.

#### 4. Bank handling financial transactions

- **Sector-specific regulations:** Applicable banking and financial-services requirements.
- **Privacy laws:** Rules governing customer information and financial data.
- **Payment-card standards:** PCI DSS may apply if the bank handles payment-card data within its scope.
- **Security standards:** ISO/IEC 27001 may support information-security management.

**Reason:** Banks must protect financial transactions and customer information while meeting applicable financial-sector requirements.

**SOX clarification:** SOX concerns corporate financial reporting and internal controls for relevant companies. It is not a general regulation for every bank's customer financial records.

**Remember:** One organisation can fall under multiple compliance categories. The exact requirements depend on its location, activities, data, and applicable legal or contractual obligations.

### Step 4 — Compliant versus secure

**Why are they different?**

Compliance means meeting applicable requirements and demonstrating that they are met. Security is the ongoing effort to protect systems, networks, applications, and information from threats.

They overlap, but meeting requirements does not guarantee that every real-world threat has been addressed. Likewise, an organisation may have strong technical safeguards but still fail a compliance requirement because it lacks required documentation or has not completed a required assessment.

**Example of being compliant but still insecure:**

An organisation passes an audit and documents all required security policies. Later, an employee account is compromised, but the security team ignores unusual login activity because it assumes the successful audit means the organisation is secure.

The organisation may have met particular requirements, but it has failed to respond to a potential threat.

**The box-ticking trap:** Focusing on proving that requirements have been met while ignoring actual risks and suspicious activity.

**The mature view: Compliance is a floor, not a ceiling.**

Compliance establishes a valuable baseline, but effective security also requires ongoing risk assessment, monitoring, investigation, and improvement.

**Why compliance still matters:**

- It establishes minimum protections.
- It helps protect people and their information.
- It creates accountability through documentation, evidence, and audits.
- It encourages organisations to invest in security.
- It helps build trust with customers, partners, and regulators.

Compliance is an important part of a security programme, but it is not a replacement for genuine security.

### Step 5 — Connect compliance to a cybersecurity career

**Why does compliance drive security work?**

Organisations need security professionals to implement required controls, monitor systems, prepare for audits, maintain documentation, collect evidence, and help meet legal, regulatory, and contractual obligations. Compliance can influence security budgets, priorities, and hiring.

**How does this knowledge help in the field and interviews?**

Understanding compliance helps security professionals recognise an organisation's obligations, understand why particular controls exist, and explain how security work supports organisational requirements. This matters even in technical roles such as SOC analyst, because monitoring and incident investigations take place within an organisation's wider security and compliance responsibilities.

In interviews, explaining why a control matters—not just naming a tool—shows an understanding of the purpose behind security work.

---

## Key takeaways

- Compliance means meeting applicable requirements and being able to demonstrate that they are met.
- Compliance exists to protect people, establish a baseline, and create accountability and trust.
- Four major categories are personal-data privacy laws, sector-specific regulations, payment-card standards, and security frameworks/standards.
- GDPR, HIPAA, PCI DSS, and ISO/IEC 27001 represent different categories; SOX is an example of a rule focused on corporate financial reporting and internal controls.
- Organisations may need to meet several requirements at the same time.
- Passing an audit does not guarantee that an organisation is secure.
- **Compliance is a floor, not a ceiling:** organisations must also manage real risks and respond to threats.
- Compliance influences security controls, priorities, budgets, audits, and cybersecurity hiring.
- Compliance knowledge is useful in technical roles and interviews because it helps explain why security controls matter.

## Connection to Day 86 — Risk management

Risk management is the broader process of identifying, assessing, prioritising, and deciding how to respond to risks. Compliance is one consideration within that broader process; meeting requirements does not remove the need to understand and manage actual risks.
