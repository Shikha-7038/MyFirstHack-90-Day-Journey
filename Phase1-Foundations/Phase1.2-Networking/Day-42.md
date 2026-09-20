# Day 42 — Wireless Network Security

**Learning Journey:** MyFirstHack — 90 Days  
**Day:** 42 of 90  
**Topic:** Wireless Network Security  
**Focus:** Evil Twin, Rogue Access Points, Deauthentication, Wi-Fi Password Attacks, WPA2/WPA3, PMF, Cellular Security, and Wireless Defense

---

## 1. Introduction

Today I learned about **wireless network security** and why Wi-Fi needs a different security mindset from wired networks.

Wireless communication travels through the air instead of through a physical cable. This makes wireless networks convenient, but it also creates additional opportunities for attackers to observe, impersonate, or disrupt connections.

The main lesson was:

> **Do not trust a wireless network simply because its name looks familiar.**

---

## 2. Why Wireless Networks Are Different

In a wired network, communication generally travels through physical cables.

In a wireless network:

**Device → Radio signal → Access Point**

The signal travels through the air and can be detected by nearby devices.

However, detecting a wireless signal does **not** automatically mean that someone can read the encrypted information being transmitted.

Wireless security therefore depends on things such as:

- Authentication
- Encryption
- Strong passwords
- Secure Wi-Fi standards
- Network segmentation
- Monitoring

---

## 3. SSID — Wi-Fi Network Name

**SSID (Service Set Identifier)** is the name displayed when we look at available Wi-Fi networks.

Examples:

- Home_WiFi
- Cafe_WiFi
- College_WiFi

An important lesson I learned was:

> **SSID is a name, not proof of identity.**

Multiple access points can use the same SSID. Therefore, seeing a familiar Wi-Fi name does not prove that the network is legitimate.

For example:

**Real:** `Cafe_WiFi`

**Fake:** `Cafe_WiFi`

This is one of the ideas behind an **Evil Twin attack**.

---

## 4. BSSID

**BSSID (Basic Service Set Identifier)** identifies a particular Wi-Fi access point/radio and is commonly associated with its MAC address.

The difference can be remembered as:

- **SSID → Network name**
- **BSSID → Particular access point/radio**

BSSID is more specific than SSID, but it should not be considered cryptographic proof that an access point is legitimate.

---

# 5. Evil Twin Attack

An **Evil Twin** is a fake wireless network designed to impersonate a legitimate Wi-Fi network.

For example:

```text
Real Wi-Fi:
Cafe_WiFi

Fake Wi-Fi:
Cafe_WiFi
```

A victim may connect to the fake network because the name looks familiar.

Once connected, the attacker may attempt to:

- Observe network metadata
- Interfere with communication
- Present a fake captive portal
- Trick users into providing credentials
- Position themselves between the victim and the Internet

### Defense

- Do not trust the SSID alone.
- Verify the correct network when possible.
- Use HTTPS.
- Use a VPN on untrusted networks.
- Never ignore certificate warnings.
- Be cautious with captive portals.
- Prefer cellular/mobile data when practical.

---

# 6. Rogue Access Point

A **rogue access point** is an unauthorized wireless access point connected to a network.

It can be installed by:

- An attacker
- An employee trying to improve Wi-Fi coverage
- Someone using an unauthorized router

A well-meaning employee can accidentally create a security weakness by connecting an unmanaged access point to the organization's network.

### Risks

A rogue AP can:

- Bypass organizational security controls
- Have weak security settings
- Remain unmonitored
- Create an unauthorized entry point

### Defense

Organizations should:

- Monitor wireless networks
- Scan for unauthorized access points
- Control which devices can connect
- Maintain policies against unauthorized networking equipment

---

# 7. Deauthentication Attacks

Wi-Fi uses **management frames** to manage connections.

Older Wi-Fi security had weaknesses where certain management messages were not properly authenticated.

An attacker could potentially forge a disconnect message and force a device off the network.

Conceptually:

```text
Victim
  ↓
Connected to Wi-Fi
  ↓
Fake disconnect message
  ↓
Disconnected
```

### Why would an attacker do this?

#### 1. Denial of Service

Repeatedly disconnect devices from the network.

#### 2. Force reconnection

Disrupt the victim's connection and potentially create an opportunity for other attacks.

The important defensive lesson is to understand that **connection-management messages themselves need protection**.

---

# 8. Protected Management Frames (PMF)

**PMF = Protected Management Frames**

PMF provides protection for certain Wi-Fi management messages.

Without appropriate protection, forged management messages can potentially interfere with a connection.

PMF helps prevent attackers from successfully using forged management frames.

A simple way to remember it:

> **PMF protects important Wi-Fi control/management messages.**

PMF is particularly relevant to protection against attacks such as forged deauthentication/disconnection messages.

---

# 9. Wi-Fi Password Attacks

When a device connects to a password-protected Wi-Fi network, the password is **not simply transmitted directly** over the air.

Instead, a cryptographic authentication process takes place.

With WPA2, an attacker who captures relevant authentication material may be able to attempt password guesses **offline**.

The basic concept is:

```text
Capture authentication exchange
              ↓
       Take it offline
              ↓
       Try password guesses
              ↓
       Check for a match
```

The attacker can perform the guessing on their own hardware rather than repeatedly interacting with the Wi-Fi router.

### Password strength matters

A weak password is easier to guess.

A long, unique and random password is significantly harder to crack.

Therefore:

> **Wi-Fi password security is an important part of network security.**

---

# 10. Evolution of Wi-Fi Security

Wireless security standards have evolved as weaknesses were discovered.

```text
WEP
 ↓
WPA
 ↓
WPA2
 ↓
WPA3
```

### WEP

WEP is considered broken and should not be used.

### WPA

An improvement over WEP, but now outdated.

### WPA2

Still widely used and generally acceptable, but has known limitations, including weaknesses around offline password guessing.

### WPA3

A newer standard designed to provide stronger security, including better resistance to offline password guessing and improved protection of management frames.

### Practical recommendation

> **Use WPA3 when supported. WPA2 is still a common acceptable option. Avoid WEP and open networks for sensitive activities.**

---

# 11. HTTPS on Untrusted Wi-Fi

HTTPS encrypts communication between a browser and a website.

Conceptually:

```text
Device
  ↓
🔒 HTTPS
  ↓
Website
```

This provides an important layer of protection even when the local Wi-Fi network cannot be fully trusted.

HTTPS is therefore especially important when using public Wi-Fi.

---

# 12. Certificate Warnings

Browsers can display warnings such as:

> **Your connection is not private**

I learned that these warnings should **not simply be ignored**.

A certificate warning can indicate a problem with the website's certificate or the connection.

### Rule:

> **Never blindly bypass certificate warnings.**

---

# 13. VPN

A VPN creates an encrypted tunnel between the device and the VPN server.

```text
Device
  ↓
🔒 Encrypted VPN tunnel
  ↓
VPN Server
  ↓
Internet
```

A VPN can reduce what an untrusted local Wi-Fi network can see or inspect.

However:

> **A VPN does not make malicious websites, phishing, or malware safe.**

It is an additional layer of protection, not a complete security solution.

---

# 14. Captive Portals

A **captive portal** is a webpage that appears when connecting to some public Wi-Fi networks.

Examples include:

- Hotels
- Airports
- Cafés

The danger is that an attacker operating an Evil Twin can create a **fake captive portal**.

Therefore, users should be careful when a Wi-Fi login page unexpectedly asks for sensitive credentials, especially passwords that are reused on other accounts.

---

# 15. Cellular Security

I also learned that wireless security is not limited to Wi-Fi.

Mobile networks such as **4G and 5G** provide another form of wireless connectivity.

In general, cellular networks are more resistant to casual attacks than unknown open public Wi-Fi.

This is one reason using:

**Mobile data / personal hotspot**

can be preferable to connecting to an unknown public Wi-Fi network.

However:

> **Cellular networks are not completely immune to attacks.**

---

# 16. IMSI Catchers

An **IMSI catcher** is equipment that can impersonate aspects of a cellular network.

It can be compared conceptually to an Evil Twin:

**Wi-Fi:**

Fake AP → imitates real Wi-Fi

**Cellular:**

Rogue equipment → imitates aspects of a cellular network

The broader lesson is:

> **No wireless medium should automatically be considered completely trustworthy.**

Strong application-layer encryption such as HTTPS and properly implemented end-to-end encryption can provide additional protection.

---

# 17. Defending Yourself on Networks You Don't Control

Examples:

- Public Wi-Fi
- Café Wi-Fi
- Hotel Wi-Fi
- Airport Wi-Fi

The correct mindset is:

> **Treat an unfamiliar network as untrusted.**

### Defenses

- Use HTTPS.
- Use a VPN when appropriate.
- Do not ignore certificate warnings.
- Be careful with captive portals.
- Don't trust the Wi-Fi name alone.
- Verify the network when possible.
- Prefer cellular/mobile data when practical.

---

# 18. Securing Networks You Control

For home or business Wi-Fi:

### Use

- WPA3 when supported
- WPA2 when WPA3 isn't available
- Strong, long Wi-Fi passwords
- Changed router administrator credentials
- Updated router firmware
- Guest networks
- IoT network separation
- Network segmentation

### Avoid

- WEP
- Open networks for sensitive activities
- Default administrator credentials
- Outdated router firmware

---

# 19. Network Segmentation

This connects directly with **Day 34 — Network Segmentation**.

A network should not necessarily put every device into one large network.

For example:

```text
                 Router
                   │
        ┌──────────┼──────────┐
        ↓          ↓          ↓
      Guest       IoT      Business
      Wi-Fi      Devices    Devices
```

For a small business, customer Wi-Fi should be separated from:

- Payment/till systems
- Back-office computers
- Other sensitive business systems

### Why?

If one network segment becomes compromised, segmentation can limit how far an attacker can move.

> **Less access can mean less potential damage.**

---

# 20. Wireless Security and Zero Trust

Today's lesson connects directly to **Day 40 — Zero Trust**.

Zero Trust teaches:

> **Never trust, always verify.**

Wireless security applies the same principle.

Instead of thinking:

> “I recognize this Wi-Fi name, so it must be safe.”

Think:

> “How do I know this network is legitimate, and what protections are in place?”

This is especially important because an SSID can be copied.

---

# 21. Practical Wireless Audit

As part of today's defensive lab, I observed the wireless networks visible around me.

### Step 1 — Wireless environment

I observed:

- **4 Wi-Fi networks**
- **4 secured networks**
- **0 open networks**
- No obvious duplicate/similar network names
- No obvious generic “Free Wi-Fi” network

This was an observation-only activity. I did not connect to any new network.

### Step 2 — Own network security

My Wi-Fi uses:

> **WPA2/WPA3-Personal**

This provides compatibility with WPA2 devices while supporting WPA3.

### Step 3 — Router configuration

The following checks still need to be completed when I am back at home:

- Router administrator password
- Router firmware update status
- Guest network availability and separation

### Step 4 — Public Wi-Fi reasoning

If I see multiple Wi-Fi networks with similar names and don't know which one is genuine, I can reduce the risk by:

- Using HTTPS
- Using a VPN
- Paying attention to certificate warnings
- Being cautious with captive portals
- Not trusting the SSID alone
- Verifying the legitimate network when possible
- Using cellular/mobile data when practical

---

# 22. Legal and Ethical Considerations

Wireless security knowledge should be used for **defensive and authorized purposes**.

### Legitimate

- Testing my own router
- Testing my own devices
- Using a cybersecurity lab
- Performing authorized security testing with permission

### Not legitimate

- Cracking someone else's Wi-Fi
- Capturing traffic from networks I don't control
- Interfering with another person's Wi-Fi
- Setting up an Evil Twin against unsuspecting users
- Performing deauthentication attacks against networks without authorization

### Rule:

> **Only test wireless networks and devices that I own or have explicit permission to test.**

---

# 23. Connection to Previous Learning

### Day 33 — Network Attacks

I learned about attacks such as MITM, ARP poisoning, DNS spoofing and DoS.

Day 42 extended this understanding to the **wireless layer**.

### Day 34 — Network Segmentation

Segmentation can limit the impact of a compromised wireless device or network segment.

### Day 40 — Zero Trust

The principle of:

> **Never trust, always verify**

applies directly to wireless networks.

### Day 41 — IPv6

Day 41 taught me that adding a new networking capability also creates security responsibilities.

Day 42 similarly showed that wireless connectivity creates another attack surface that must be secured and monitored.

---

# 24. Key Takeaways

1. Wireless signals travel through the air and create an additional attack surface.
2. An **SSID is a name, not proof of identity**.
3. An **Evil Twin** impersonates a legitimate Wi-Fi network.
4. A **rogue AP** is an unauthorized wireless access point.
5. **Deauthentication attacks** can disrupt wireless connections.
6. **PMF** helps protect Wi-Fi management frames.
7. WPA2 authentication material can potentially support offline password guessing.
8. Strong, long Wi-Fi passwords are important.
9. **WPA3 is preferred**, while WPA2 remains widely used.
10. WEP and open networks should be avoided for sensitive activities.
11. HTTPS provides protection even when the local network is untrusted.
12. VPNs provide another layer of protection on untrusted networks.
13. Certificate warnings should never be blindly ignored.
14. Cellular is generally preferable to unknown public Wi-Fi, but it is not completely immune to attacks.
15. Network segmentation can limit the impact of a compromised device.
16. Wireless security follows the Zero Trust principle: **don't trust simply because something looks familiar — verify it.**
17. Security testing must always be performed on your own equipment or with explicit authorization.

---

# 25. Final Reflection

Today I learned that wireless security is not simply about protecting a Wi-Fi password.

It is about understanding **who I am connecting to, how that connection is authenticated, how communication is protected, and what happens if the network itself cannot be trusted**.

The most important lesson I am taking from Day 42 is:

> **“SSID is a name — not proof of identity.”**

And the principle that connects today's lesson with Zero Trust is:

> **“Never trust, always verify.”**