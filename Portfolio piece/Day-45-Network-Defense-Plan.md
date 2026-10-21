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
