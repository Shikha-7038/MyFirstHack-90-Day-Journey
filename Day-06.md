# Day 6 – Understanding IP Addresses & Online Privacy

**Date:** July 29, 2026

## 🎯 Objective

Learn how IP addresses work, what information websites can collect from them, and why they are important in networking and cybersecurity.

---

# 📚 Key Learnings

## What is an IP Address?

- A unique numerical identifier assigned to a device on a network.
- Enables devices to send and receive data over the Internet.
- Every Internet-connected device requires an IP address to communicate.

**Example:**

```text
192.168.1.10
```

---

## Types of IP Addresses

### 🌐 Public IP Address

- Assigned by the Internet Service Provider (ISP).
- Used for communication over the Internet.
- Visible to websites and online services.
- Can change depending on the ISP's configuration (dynamic IP).

### 🏠 Private IP Address

- Assigned within a local network.
- Used for communication between devices on the same network.
- Not directly accessible from the Internet.
- Multiple devices can share one public IP through a router.

---

## Information Websites Can See

When visiting a website, it can automatically detect:

- Public IP address
- Approximate location (city/region)
- ISP
- Browser
- Operating System
- Device type
- Time zone

> **Observation:** This information is shared automatically during network communication without filling out any forms.

---

## IP Geolocation

- IP addresses do **not** reveal an exact home address.
- They usually identify only an approximate city or region.
- Accuracy depends on the ISP and the geolocation database being used.

---

## VPN and Tor

### 🔒 VPN

- Replaces the original public IP with the VPN server's IP.
- Helps improve privacy by hiding the user's real public IP.

### 🧅 Tor

- Routes traffic through multiple relay nodes.
- Websites only see the Tor exit node's IP address.
- Provides stronger anonymity than simply exposing the original public IP.

---

## 🧪 Practical Activity

Used an online IP lookup tool to observe:

- Public IP address
- ISP
- Approximate location
- Time zone
- Network details

### Observation

- The displayed location was approximate rather than an exact address.
- This demonstrated how much information websites can infer from a simple connection.

---

## 🛡️ Why This Matters in Cybersecurity

IP addresses help security professionals to:

- Monitor network traffic.
- Investigate suspicious activities.
- Detect unauthorized access attempts.
- Analyze attack sources.
- Support digital forensic investigations.

---

## ✅ Key Takeaways

- Every Internet-connected device needs an IP address.
- Public IP addresses are assigned by ISPs, while private IP addresses are used inside local networks.
- Websites automatically receive a visitor's public IP during communication.
- IP-based geolocation provides an approximate location, not a precise address.
- VPNs and Tor protect privacy by hiding the original public IP in different ways.
- Understanding IP addresses is a foundational networking skill for cybersecurity.

---

## 💭 Reflection

- Learned that an IP address is more than just a device identifier; it is essential for Internet communication.
- Corrected the misconception that an IP address reveals an exact physical address.
- Gained a better understanding of how websites identify visitors and how privacy tools such as VPNs and Tor help protect user identity.
- This lesson strengthened my networking fundamentals, which will support future topics like DNS, routing, packet analysis, and digital forensics.

---

## 📈 Progress

**Day 6 of 90 ✔️**