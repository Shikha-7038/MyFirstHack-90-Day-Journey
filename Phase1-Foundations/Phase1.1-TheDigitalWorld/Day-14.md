# 🛡️ Day 14 Journey – Home Wi-Fi Security

## 📖 Overview

Day 14 focused on understanding how home Wi-Fi networks work and why securing a router is just as important as securing the devices connected to it. I learned that network security starts below the web layer. Even though HTTPS protects data during transmission, the router remains the first security boundary for every device on a network.

Today's learning also introduced common Wi-Fi security standards, router security practices, public Wi-Fi risks, and the importance of keeping networking equipment updated.

---

# 📚 What I Learned

## 🌐 1. A Router Does More Than Provide Wi-Fi

Before today, I thought a router's main purpose was simply to provide internet access.

I learned that a router performs several important functions:

- 🌍 Connects the home network to the ISP.
- 📡 Assigns IP addresses to connected devices using DHCP.
- 🔎 Handles DNS requests.
- 🛡️ Works as a firewall by blocking unwanted incoming traffic.
- 📶 Broadcasts the Wi-Fi network.

**💡 Learning:** This helped me understand why the router is considered the security gateway of an entire home network.

---

## 🔑 2. Wi-Fi Password vs Router Admin Password

One of the biggest lessons today was learning that these are completely different passwords.

### 📶 Wi-Fi Password

- Used by devices to connect to the wireless network.

### ⚙️ Router Admin Password

- Used to access and change router settings.
- Controls security settings, firmware updates, DNS configuration, guest networks, and more.

**💡 Learning:** Many people only change their Wi-Fi password while leaving the router's administrator password unchanged, which creates a serious security risk.

---

## 🔒 3. Understanding Wi-Fi Security Protocols

I learned the evolution of Wi-Fi encryption.

### ❌ WEP

- Very old.
- Easily broken.
- Should never be used.

### ⚠️ WPA

- Better than WEP.
- Still outdated.

### ✅ WPA2 (AES)

- Still widely used.
- Secure when properly configured.

### ⭐ WPA3

- Current recommended standard.
- Provides stronger authentication and better protection.

**💡 Learning:** Using modern encryption standards is just as important as choosing a strong password.

---

## 🌍 4. Why Wi-Fi Encryption Is Still Important

Initially I wondered:

> **"If HTTPS already encrypts websites, why does Wi-Fi also need encryption?"**

I learned that HTTPS only encrypts website communication.

Wi-Fi encryption also protects:

- 📡 Local network traffic.
- 🖨️ Devices like printers, smart TVs, cameras, and IoT devices that may not use HTTPS.
- 📊 Network metadata such as which websites are being visited.

**💡 Learning:** HTTPS and Wi-Fi encryption work together to improve overall security.

---

## 🚨 5. KRACK Vulnerability

Today I learned about the **KRACK attack**.

Important points:

- ⚠️ It targeted WPA2.
- 🔓 Attackers didn't need the Wi-Fi password.
- 🧩 It exploited a weakness in the WPA2 protocol.
- 🔄 Vendors released security patches.
- 📱 Devices that never received updates may still be vulnerable.

**💡 Learning:** Firmware updates are essential because protocol vulnerabilities can affect millions of devices.

---

## ☕ 6. Public Wi-Fi Risks

Previously, I believed public Wi-Fi was dangerous because attackers could directly read passwords.

Today's lesson explained that HTTPS has greatly reduced this risk.

However, public Wi-Fi still presents threats such as:

- 📡 Evil Twin Wi-Fi networks.
- 🌐 DNS manipulation.
- ⚠️ Captive portal abuse.
- 👀 Metadata collection.

**💡 Learning:** Modern public Wi-Fi attacks focus more on network manipulation than reading encrypted data.

---

## 🏠 7. Home Router Security Checklist

I learned that a security analyst usually checks:

- 🔑 Router administrator password.
- 🔒 Wi-Fi encryption mode.
- 🔐 Wi-Fi password strength.
- 🔄 Firmware version.
- 👥 Guest network availability.
- 🌍 Remote management settings.
- 💻 Connected devices.

**💡 Learning:** A simple checklist can quickly identify the most common security weaknesses in a home network.

---

# 🧪 Practical Activity 1 – Router Audit

The practical task required logging into a router's administration page.

### 📝 My Experience

- I first tried accessing the default gateway of my hostel Wi-Fi.
- The login page appeared, but it required administrator credentials because the hostel network is centrally managed.
- I then connected my laptop to my mobile hotspot and tried accessing its default gateway.
- Since a mobile hotspot only shares internet and does not function as a traditional configurable home router, there was no router administration page available.

### 📌 Findings

Although I couldn't perform the complete router audit, I learned:

- 🏢 Shared hostel networks are managed by administrators.
- 📱 Mobile hotspots are different from traditional home routers.
- 🚫 Not every network allows users to access router settings.

---

# 💡 Practical Activity 2 – Understanding Routers

While completing today's lesson, I realized I had been confusing **Wi-Fi** with **routers**.

### What I Learned

- 📶 Wi-Fi is the wireless technology used to connect devices.
- 🌐 A router is the networking device that creates and manages the network.

This also helped me understand why my home does not have a traditional router—everyone uses their own mobile data instead of a shared broadband connection.

---

# 🔐 Practical Activity 3 – Password Strength Testing

I tested different password styles using a password strength checker.

### 📊 Results

| Password Type | Estimated Crack Time |
|---------------|----------------------|
| 🔹 Password similar to my current password | **~1 trillion years** |
| 🔹 Random 16-character password | **~5 undecillion years** |
| 🔹 Passphrase (`correct-horse-battery-staple-table`) | **Extremely high (practically impossible with current computing)** |

### 💡 Learning

- Long random passwords provide excellent protection.
- Long passphrases are both secure and easier to remember.
- Password length is one of the biggest factors affecting password strength.

---

# 🤔 Questions I Explored Today

While performing today's activities, I also explored a few additional questions.

### ❓ Is Wi-Fi the same as a router?

**Answer:** No.

- 📶 Wi-Fi is the wireless connection.
- 🌐 A router is the device that creates and manages the network.

---

### ❓ Why couldn't I access the router settings from my phone hotspot?

Because a mobile hotspot shares internet from a phone but usually doesn't provide a configurable router administration interface like a broadband router.

---

### ❓ Should I try accessing every router's default gateway?

I learned that accessing the default gateway of a network **you are authorized to use** is normal.

However:

- Seeing a login page is expected.
- Logging in without permission is not allowed.
- If a router allows administrative access without authentication, it should be reported to the owner or administrator rather than explored further.

---

# 😲 What Surprised Me

The things that surprised me the most were:

- 🤯 A router performs many more security functions than simply providing Wi-Fi.
- 🔑 The administrator password is often more important than the Wi-Fi password.
- 🛡️ WPA3 is recommended because even WPA2 experienced protocol-level vulnerabilities like KRACK.
- 🔄 Firmware updates are critical for protecting routers against newly discovered vulnerabilities.
- ⏳ Very long passwords and passphrases can require astronomical amounts of time to brute-force.

---

# 🎯 Key Takeaways

- ✅ Home network security starts with securing the router.
- ✅ Router administrator passwords should always be changed from default values.
- ✅ WPA3 is the preferred Wi-Fi encryption standard, while WEP and WPA should never be used.
- ✅ Firmware updates protect routers from newly discovered vulnerabilities.
- ✅ Guest networks help isolate visitors and IoT devices from personal systems.
- ✅ Strong passwords and passphrases significantly increase resistance against brute-force attacks.
- ✅ HTTPS protects website communication, while Wi-Fi encryption protects the local network.
- ✅ Understanding routers and home networks is an important foundation for cybersecurity professionals.

---

# 📝 Conclusion

This documentation reflects both the concepts I studied and the practical tasks I attempted today. Even though I could not access a router administration panel due to using a managed hostel network and a mobile hotspot, I gained a much better understanding of routers, Wi-Fi security, encryption standards, password strength, and home network defenses.

🚀 Every lesson helps me build stronger cybersecurity fundamentals and prepares me for more advanced topics in the coming days.