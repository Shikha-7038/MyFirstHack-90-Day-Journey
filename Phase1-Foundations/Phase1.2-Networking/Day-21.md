# 🌐 Day 21 of 90 – Understanding Networks

**Phase 1.2: Networks**

Today I started Phase 1.2 of my 90-day cybersecurity journey. The focus shifted from understanding cybersecurity threats to understanding how data actually moves between devices.

## 🧠 What I Learned Today

The simplest definition of a network that I learned today is:

> **A network is two computers having a conversation.**

Although networks can become very complicated, the basic idea remains the same.

Every network conversation has four important parts:

1. 👤 **Sender** – the device that starts the communication.
2. 🎯 **Receiver** – the device or service receiving the communication.
3. 🗣️ **Protocol** – the common language used for communication, such as HTTP, HTTPS, DNS, TCP, or UDP.
4. 🛣️ **Route** – the path that the data follows between the sender and receiver.

This gave me a much easier way to understand networking. Instead of trying to memorize many networking terms separately, I can now think about every communication as a conversation between two devices or services.

### 🌍 The Same Model at Different Scales

I learned that this model works at different scales:

- 💻 Two computers communicating directly
- 🏠 Devices communicating through a home/local network
- 🌐 Devices communicating across the internet
- ☁️ Applications communicating with multiple online services

The basic model stays the same. The main difference is the complexity of the route and the number of devices and services involved.

### 🛡️ Where Attackers Can Target the Conversation

From a cybersecurity perspective, attackers can target different parts of a network conversation.

- 👤 **Sender:** spoofing or impersonation
- 🎯 **Receiver:** DoS/DDoS attacks
- 🗣️ **Protocol:** DNS poisoning and protocol-level attacks
- 🛣️ **Route:** Man-in-the-middle attacks and evil-twin Wi-Fi attacks

This helped me understand network attacks as part of a structured model instead of seeing them as unrelated cybersecurity terms.

---

## 🔍 Practical Task 1 – Network Device Observation

The original exercise asked me to inventory devices on my home network.

Since I was connected to a **shared hostel Wi-Fi network that I do not manage**, I did not try to identify or scan other people's devices. Instead, I limited the exercise to my own devices.

### 📱💻 My Own Devices

I identified two of my own devices connected to the hostel Wi-Fi:

- 💻 Windows laptop
- 📱 Android phone

I checked the network information on my Windows laptop and found:

- **IPv4 address:** `192.168.160.x` *(exact address kept private)*
- **Subnet mask:** `255.255.248.0`

I also checked my phone and found that its IP address began with `192.168.160`. My phone did not show the subnet mask in its normal Wi-Fi settings.

### 🔐 Important Security Learning

One important thing I learned from this task was that I should not automatically assume that the devices I personally identify represent the total number of devices on a shared network.

There could be many other devices connected to the hostel network.

Because the network was not mine to manage, I kept the assessment within my own devices. This helped me understand an important cybersecurity concept:

> **Always define the scope of an assessment before investigating a network.**

### 📌 My Safe Inventory Finding

> I identified two of my own devices connected to the shared hostel Wi-Fi. I did not enumerate or investigate other users' devices because I do not manage the network.

---

## 🌐 Practical Task 2 – Counting Webpage Network Requests

The second practical task was to see how many network conversations can happen when loading just **one webpage**.

### 🧪 First Test – Wikipedia

I initially tested Wikipedia.

The page generated:

- **6 requests**
- All observed requests were associated with `www.wikipedia.org`
- **Unique domains:** 1

This showed me that different websites can behave very differently.

### 🧪 Second Test – BBC

I then tested the BBC website because it provided a better example for understanding the concept.

Using the browser's **Developer Tools → Network** tab, I observed the requests generated when the BBC webpage loaded.

### 📊 My Results

| Finding | Result |
|---|---|
| 🌐 Website tested | BBC |
| 📊 Total requests | **155** |
| 📦 Data transferred | **175 kB** |
| 📚 Resources | **9.9 MB** |
| ⏱️ Finish | **11.87 seconds** |
| ⚡ DOMContentLoaded | **2.16 seconds** |
| ⚡ Load | **3.72 seconds** |
| 🔗 Unique domains observed | **6** |

### 🔗 Domains I Observed

1. `www.bbc.com`
2. `cdn.optimizely.com`
3. `cdn.tinypass.com`
4. `www.bbc.co.uk`
5. `edigitalsurvey.com`
6. `ping.chartbeat.net`

### 😮 My Observation

I did not have one specific domain that surprised me because I was unfamiliar with the non-BBC domains in general.

My main observation was that I expected a webpage to mainly communicate with the website I had opened, but the browser actually contacted several different domains while loading the page.

This helped me understand the difference between what I see on a webpage and what is happening behind the scenes.

### 📌 Main Practical Finding

> **One BBC webpage generated 155 network requests and contacted 6 unique domains.**

The lesson also mentioned that the median webpage in 2024 required around **71 requests**. My BBC test generated considerably more requests, which helped me understand that the number of requests can vary significantly depending on the website and what it loads.

---

## 💡 What I Learned From the Practical Work

Before today's lesson, I mostly thought about visiting a website as something simple:

> **I open a website → my browser communicates with that website.**

Today I understood that a webpage can involve many separate network conversations happening behind the scenes. Different resources and services can require different requests and connections.

The BBC test made this especially clear to me. One webpage generated **155 requests**, even though from my perspective I had only opened one website.

I also learned that networking is not just about memorizing IP addresses, ports, protocols, and other terms. The **sender → receiver → protocol → route** model gives me a way to connect these concepts together.

Another important lesson was about **security scope**. When I wanted to perform the network inventory task on hostel Wi-Fi, I realized that I should not investigate devices belonging to other people just because they are on the same network. I could safely examine my own devices and document the limitation.

---

## 📝 Key Takeaway

Today I learned to look at the internet as a collection of **network conversations** rather than simply websites and applications.

The biggest practical finding was:

> 🌐 **One BBC webpage → 155 network requests → 6 unique domains**

This showed me that a webpage is not a single conversation but a collection of conversations happening behind the scenes.

I also learned that a cybersecurity assessment should have a clear scope. Since the hostel Wi-Fi was shared and not managed by me, I kept my practical investigation limited to my own devices.

Today gave me the foundation for the next part of the networking phase, where I will learn more about **IP addresses, ports, DNS, TCP, UDP, packets**, and eventually how to inspect real network traffic.

---

### 🚀 Next

**Phase 1.2 continues — Networks**

The next lessons will build on today's conversation model and gradually move toward understanding how actual network traffic works.

**Day 21/90 complete.** ✅
