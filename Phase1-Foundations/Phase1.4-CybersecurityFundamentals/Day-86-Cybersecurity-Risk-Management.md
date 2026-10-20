# Day 86 — Cybersecurity Risk Management

## Overview

Cybersecurity risk management is the process of identifying, assessing, prioritising, and responding to risks that could affect an organisation’s systems, data, people, and operations.

The goal is not to eliminate every possible risk. Threats change, and organisations have limited time, money, and personnel. The aim is to reduce risks to an acceptable level and focus resources on what matters most.

## 1. The Risk Management Cycle

### Step 1: Identify the risk

Determine what needs protection, what could go wrong, and which threats or vulnerabilities could affect the organisation.

- **Assets:** Things of value, such as customer databases, applications, devices, and networks.
- **Threats:** Potential causes of harm, such as phishing, ransomware, malicious insiders, or unauthorised access.
- **Vulnerabilities:** Weaknesses that could be exploited, such as outdated software, weak passwords, or misconfigured systems.
- **Consequences:** Possible outcomes, including data exposure, financial loss, operational disruption, or reputational damage.

**Example:** A customer database runs outdated software. The outdated software is a vulnerability; an attacker exploiting it is a possible threat scenario.

### Step 2: Assess the risk

Evaluate how likely an event is and how serious its consequences could be.

- **Likelihood:** How likely is the event to happen?
- **Impact:** How much damage could it cause?

A common conceptual model is:

`Risk ≈ Likelihood × Impact`

This is a useful simplification; real assessments may use more detailed scoring methods.

A likely phishing attack that could expose sensitive customer information may deserve more urgent attention than a minor weakness in an isolated test environment. Prioritisation should consider both likelihood and impact, along with the context of the affected asset.

### Step 3: Choose a response

Organisations commonly respond to risks in four ways: mitigate, accept, transfer, or avoid.

#### Mitigate

Reduce the likelihood of a risk, its impact, or both.

Examples:
- Patch vulnerable software.
- Enable multi-factor authentication (MFA).
- Train employees to recognise phishing.
- Segment networks to limit the spread of an attack.
- Restrict access to sensitive information.

Mitigation reduces risk but does not always eliminate it.

#### Accept

Consciously retain a risk rather than adding more controls.

This may be appropriate when the risk is within approved limits and further controls would not justify their cost. Acceptance should be informed, documented when appropriate, and approved by the right person—not simply ignored.

#### Transfer

Shift or share some of the financial or other consequences with another party.

Examples include cyber insurance for certain eligible losses or contracts that allocate specific responsibilities to a service provider.

Transfer does not remove the underlying risk or eliminate the organisation’s responsibility for protecting systems and data. Insurance may also have exclusions and limits.

#### Avoid

Stop the activity that creates the risk.

Examples:
- Do not collect sensitive data that the business does not need.
- Discontinue an insecure service that cannot be adequately protected.
- Do not introduce a feature that creates an unacceptable security exposure.

Avoidance removes the exposure associated with that activity, though other risks may remain.

### Step 4: Monitor and review

Risk management continues after a control is implemented. Organisations should review risks because threats, vulnerabilities, systems, and business needs change.

Review activities may include:
- Checking whether controls remain effective.
- Monitoring new vulnerabilities and attack techniques.
- Reassessing risks when systems or processes change.
- Updating priorities when the potential impact changes.

## 2. Comparing the Four Risk Responses

| Response | Purpose | Example |
|---|---|---|
| **Mitigate** | Reduce likelihood or impact | Patch vulnerable software |
| **Accept** | Consciously retain the risk | Accept a documented, manageable risk |
| **Transfer** | Share certain consequences | Obtain suitable cyber insurance |
| **Avoid** | Stop the risk-producing activity | Stop collecting unnecessary sensitive data |

The suitable response depends on the risk, available controls, cost, business needs, and the organisation’s risk tolerance.

## 3. Risk Prioritisation

Organisations usually cannot address every security issue at the same time. Risk prioritisation helps them decide what needs attention first.

Factors can include:
- Likelihood of the event or exploitation.
- Severity of potential consequences.
- Importance and sensitivity of affected assets.
- Existing safeguards.
- Cost and effort required to reduce the risk.
- Legal, regulatory, and business requirements.

A vulnerability that could expose customer data may need attention before a minor weakness with limited consequences. However, likelihood alone—or impact alone—does not tell the whole story. The context matters.

**Principle:** Allocate security resources according to assessed risk rather than treating every issue as equally urgent.

## 4. Risk Management as a Business Decision

Cybersecurity is also a business decision. Security investments compete with other priorities, such as development, research, operations, and staffing. No organisation has unlimited resources.

### Leadership’s role

Leadership establishes the organisation’s **risk appetite**: the level and types of risk it is willing to accept while pursuing its objectives. Leadership also sets business priorities and makes or approves significant risk and investment decisions.

### Security team’s role

Security teams support informed decisions by:
- Identifying and assessing risks.
- Explaining potential consequences in business terms.
- Recommending suitable controls.
- Monitoring whether controls are effective.
- Reporting changes in risk exposure.

The responsibilities differ: security teams provide technical assessment and recommendations, while authorised business leaders decide what level of risk is acceptable and how resources should be allocated.

## 5. Risk Appetite and Acceptable Risk

- **Risk appetite:** The amount and type of risk an organisation is prepared to take in pursuit of its objectives.
- **Acceptable risk:** Risk that falls within the organisation’s established tolerance, considering its circumstances, obligations, and priorities.

Different organisations may have different risk appetites. For example, a business handling highly sensitive financial or personal data may have a lower tolerance for certain data-exposure risks than an organisation operating a non-critical internal tool.

Accepting a risk does not mean ignoring it. The decision should be justified, recorded when appropriate, and reviewed when conditions change.

## 6. Security Controls and Risk

Security controls are measures used to prevent incidents, detect suspicious activity, or reduce the impact of incidents.

- **Preventive controls:** MFA, access restrictions, secure configuration, and patching.
- **Detective controls:** Security monitoring, audit logs, and intrusion detection systems.
- **Corrective and recovery controls:** Incident response procedures, system restoration, and tested backups.

Risk assessment helps determine which controls are appropriate and where they are likely to provide the greatest benefit. More controls do not automatically mean better security; controls should address meaningful risks and be proportionate to potential consequences.

## 7. End-to-End Process

1. **Identify** assets, threats, vulnerabilities, and potential consequences.
2. **Assess** likelihood and impact.
3. **Prioritise** risks based on significance and context.
4. **Respond** by mitigating, accepting, transferring, or avoiding each risk.
5. **Monitor and review** risks and controls as conditions change.

---

## Tasks — Think Like a Risk Manager

### Scenario

A company has limited security resources and three issues to consider:

- **Risk A:** Repeated phishing attempts target the finance team and could expose customer data.
- **Risk B:** A system has outdated software that could be exploited.
- **Risk C:** A minor weakness exists in an isolated test environment, with limited potential impact.

### Task 1: Assess and prioritise

For each risk, consider:
- How likely is it to happen or be exploited?
- What could the impact be?
- Which risk would you investigate or address first, and why?

### Task 2: Choose a response

Choose a suitable response—mitigate, accept, transfer, or avoid—for each risk. Explain your reasoning. More than one response may be reasonable depending on additional facts.

### Task 3: Select controls

Suggest one or more practical controls for the risks you would prioritise. Consider both reducing the chance of an incident and limiting its impact.

### Task 4: Explain the business decision

Explain how leadership and the security team should work together when deciding how to allocate limited security resources.

### Task 5: Review the decision

Describe what could change your assessment and how you would monitor whether the chosen controls remain effective.

---

## Key Takeaways

- Risk management aims to reduce risks to an acceptable level, not to promise zero risk.
- Likelihood and impact are central to assessing and comparing risks.
- The four common risk responses are **mitigate, accept, transfer, and avoid**.
- Transfer can share some consequences, but it does not eliminate the underlying risk.
- Risk prioritisation helps organisations use limited resources where they matter most.
- Leadership sets risk appetite and makes business decisions; security teams assess risks and recommend controls.
- Risk management is continuous because threats, vulnerabilities, controls, and business priorities change.
- Effective security is not simply about adding more controls; it is about making informed, proportionate decisions.
