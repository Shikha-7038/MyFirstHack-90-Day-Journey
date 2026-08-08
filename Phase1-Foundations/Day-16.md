# Day 16 – Mobile Security & Personal Phone Audit

**Date:** 8 August 2026  
**Day:** 16 of 90  
**Topic:** Mobile Security

---

## 🎯 Today's Objective

Understand why mobile security is different from desktop security and perform a practical security audit of my own phone.

---

## 📱 What I Learned About Mobile Security

A mobile phone is not simply a smaller computer. It has a different security model because of:

- App sandboxing
- App permissions
- Mobile operating-system updates
- Messaging-based attacks
- Biometric authentication
- The large amount of personal information stored on one device

My phone is connected to many important parts of my digital life, including:

- Email
- Banking
- Social media
- Two-factor authentication
- Photos
- Personal information
- Payment applications

Because of this, securing my phone also means protecting many other accounts.

---

## 🔹 Why Mobile Is Different From Desktop

I learned that mobile devices have several important security differences from computers:

1. **App sandboxing**
   - Apps are generally isolated from each other.
   - One app normally cannot freely access another app's data.

2. **Permission-based access**
   - Apps request access to features such as the camera, microphone, location, contacts, and photos.
   - This makes permission management an important part of mobile security.

3. **Manufacturer-controlled updates**
   - The availability of security updates depends on the device manufacturer and model.
   - An unsupported phone can remain exposed to known vulnerabilities.

4. **Messaging as an attack surface**
   - Mobile attacks often arrive through SMS, WhatsApp, QR codes, and other messaging platforms.

5. **Biometric authentication**
   - Fingerprint and face unlock make authentication convenient, but the device still relies on a PIN/password as an important backup.

---

## 🚨 Common Mobile Attacks

### 1. Smishing

Phishing through SMS messages.

Examples:

- Fake parcel delivery messages
- Fake bank alerts
- Fake account suspension messages
- Fake prize/reward messages

### 2. Malicious Apps

Apps that appear legitimate but may perform harmful activities in the background.

### 3. Sideloading

Installing applications from outside official app stores.

This can increase the risk of installing malware because the application may not have gone through the normal store-security checks.

### 4. Public Wi-Fi Attacks

Phones may automatically connect to previously used networks. Attackers can create networks with familiar names to trick devices into connecting.

### 5. Lost or Stolen Phones

An unlocked phone can provide access to:

- Email
- Banking
- Messages
- Photos
- Password managers
- Authentication methods

### 6. Zero-Click Attacks

I learned that some advanced attacks can compromise a device without the victim clicking a link or interacting with anything.

---

## 🕵️ Pegasus Case Study

I learned about Pegasus spyware and how advanced mobile attacks have been used against high-value targets such as journalists, activists, lawyers, and politicians.

The main lesson I took from the Pegasus example was:

> **Zero-click mobile attacks are possible.**

Some advanced vulnerabilities can be exploited without normal user interaction.

This also showed me why keeping the operating system and messaging applications updated is important.

---

# 🔐 Personal Mobile Security Audit

I performed a six-point security audit on my own phone.

---

## 1. 📱 Operating System

I checked my phone's software status.

**Result:**

> "Your software is up to date."

- No pending system updates were shown.
- My phone is currently up to date.

### Finding

I learned that checking for updates should be part of a security audit because outdated software can contain known vulnerabilities.

---

## 2. 🔑 App Permissions

I reviewed permissions for different categories such as:

- Camera
- Location
- Contacts
- Photos
- Microphone

### 📷 Camera Permission

I found:

- Camera → Allowed while in use
- Chrome → Allowed while in use
- Google → Allowed while in use
- Messages → Allowed while in use
- Phone → Allowed while in use
- Snapchat → Allowed while in use
- WhatsApp → Allowed while in use
- Authenticator → Ask every time
- Gmail → Ask every time
- LinkedIn → Ask every time

### 📍 Location Permission

I found:

- Google → Allowed all the time
- Camera → Allowed while in use
- Chrome → Allowed while in use
- Android Auto → Allowed while in use
- ShareMe → Allowed while in use
- Vi → Allowed while in use
- WhatsApp → Allowed while in use
- Maps → Allowed while in use
- Nykaa → Ask every time
- Paytm → Ask every time

My phone's main **Location setting is currently OFF**.

### What I Learned

I learned that an app having location permission does not automatically mean it is constantly using my location.

For example:

- **Allowed while in use** → the app can use the permission while I am using it.
- **Allowed all the time** → the app can potentially use the permission even when I am not actively using it, depending on the permission and Android behavior.

I also learned that keeping Location OFF can improve privacy, but it can reduce the availability of location-based features.

### Permission Finding

I did **not** revoke a permission during this audit.

Instead of creating a finding just to complete the task, I documented the permissions I reviewed and identified them as something I should continue monitoring.

---

## 3. 🔒 Lock Screen Security

My phone currently uses:

- 6-digit PIN
- Fingerprint
- Face unlock

I also have automatic screen locking enabled.

### What I Learned

I initially thought having a PIN, fingerprint, and face unlock meant that all three were required together.

I learned that they are alternative authentication methods:

> **PIN OR fingerprint OR face unlock → phone access**

The PIN is still important because it acts as a backup authentication method and may be required by the phone in certain situations.

I also learned that a predictable PIN such as a birthday or `123456` would weaken the overall security.

---

## 4. 🔐 Two-Factor Authentication

I checked the security settings of my Google account.

### Current Authentication

- Google Prompt
- Phone number

### Other Available Options

- Authenticator App
- Passkey
- Security Key

### What I Learned

I learned that having a phone number as a verification method is not necessarily the strongest form of 2FA.

SMS-based authentication can be affected by risks such as **SIM swapping**.

Stronger alternatives can include:

- Authenticator apps
- Passkeys
- Security keys

### Planned Improvement

I want to set up a **Passkey** for my Google account as an additional strong authentication method.

---

## 5. 📦 App Inventory

I reviewed the applications installed on my phone.

I identified applications that I no longer use and:

> **Uninstalled 4 apps.**

### What I Learned

Removing unused apps is not only about freeing storage.

Every unnecessary application is another piece of software that:

- Could contain vulnerabilities
- Could request permissions
- Could stop receiving updates
- Increases the overall attack surface

This made me understand why regular app cleanup is also part of mobile security.

---

## 6. 📍 Find Hub

I couldn't find the older **"Find My Device"** wording on my phone.

Instead, I found **Find Hub**.

I checked:

> **Allow device to be located → ON**

### Important Observation

My settings are:

- Main phone Location → **OFF**
- Find Hub "Allow device to be located" → **ON**

I learned that these settings are related but are not exactly the same.

Keeping the main Location setting OFF can improve privacy, but location-based features may not work fully when they are needed.

---

# 🛠️ My Practical Changes

During this audit, I:

- [x] Checked my OS update status
- [x] Reviewed camera permissions
- [x] Reviewed location permissions
- [x] Reviewed other important app permissions
- [x] Confirmed my 6-digit PIN
- [x] Confirmed fingerprint authentication
- [x] Confirmed face unlock
- [x] Checked Google authentication methods
- [x] Removed **4 unused apps**
- [x] Verified Find Hub's **"Allow device to be located"** setting is ON

---

# 💡 What Surprised Me

One thing that surprised me was how many different permissions I had to think about.

Before this audit, I mostly thought of permissions as something apps ask for during installation.

After checking them individually, I understood that permissions should be reviewed based on:

> **"Does this app actually need this permission to do its job?"**

I also realized that phone security is not just about having a password.

It includes:

- OS updates
- Permission management
- Strong screen lock
- 2FA
- App cleanup
- Lost-device protection

---

# 🔧 Things I Want to Improve

- [ ] Set up a Passkey for my Google account
- [ ] Continue reviewing app permissions regularly
- [ ] Avoid giving unnecessary permissions to apps
- [ ] Keep the phone and apps updated
- [ ] Regularly remove applications I no longer use

---

# 🧠 Key Takeaways

- A phone is a major part of my digital security, not just a communication device.
- Mobile security is different from desktop security.
- App permissions should be based on necessity.
- Keeping software updated reduces exposure to known vulnerabilities.
- A strong PIN combined with biometrics provides good protection.
- Strong authentication methods such as passkeys can reduce dependence on SMS.
- Removing unused apps can reduce the attack surface.
- Find Hub is important if the phone is lost or stolen.
- Keeping Location OFF can improve privacy, but there is a trade-off with location-based features.
- Mobile security should be a **regular habit**, not a one-time check.

---

# 📝 Final Reflection

Today's task was different from simply learning a cybersecurity concept because I actually applied the concepts to my own phone.

The biggest lesson for me was that mobile security is made up of many small decisions.

A secure phone is not created by one setting. It comes from:

**Updates + Permissions + Strong Lock + 2FA + App Management + Lost-Device Protection**

This made mobile security feel much more practical because I could see how the concepts from today's lesson applied directly to a device I use every day.