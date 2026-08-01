# Day 5 – How the Internet Works

**Date:** July 28, 2026

## 🎯 Objective

Understand what happens behind the scenes when a user enters a website address into a browser and how data travels across the Internet.

---

# 📚 Key Learnings

## 🌐 What Happens When We Enter a Website URL?

- The browser first checks whether it already knows the website's IP address.
- If the IP address is not available locally, a DNS lookup is performed.
- DNS translates the human-readable domain name into an IP address.
- Once the IP address is obtained, the browser establishes a connection with the destination server.
- The browser sends an HTTP or HTTPS request.
- The server processes the request and sends back the requested resources.
- The browser renders the webpage for the user.

---

## 📖 Domain Name System (DNS)

- DNS acts as the Internet's phonebook.
- It converts domain names into IP addresses.
- Without DNS, users would have to remember IP addresses instead of website names.
- Browsers and operating systems store recently visited DNS records in a cache to improve performance.

---

## 🚀 Journey of a Request

A typical web request follows this path:

1. User Device
2. Router
3. Internet Service Provider (ISP)
4. Multiple Routers across the Internet
5. Destination Server

After processing the request, the server sends the response back through a similar path.

---

## 📦 Packets

- Data sent over the Internet is divided into smaller units called **packets**.
- Each packet contains source and destination information.
- Packets may travel through different routes before reaching the destination.
- The receiving device reassembles the packets into the original data.

---

## 🔒 HTTP and HTTPS

### HTTP

- Used for communication between browsers and web servers.
- Data is transmitted without encryption.

### HTTPS

- Uses TLS/SSL encryption.
- Protects sensitive information during transmission.
- Prevents attackers from easily reading intercepted traffic.

---

## 🖥️ Key Networking Components

### Browser

- Sends requests to web servers.
- Displays the received webpage.

### Router

- Connects local devices to other networks.
- Forwards packets toward their destination.

### Switch

- Connects devices within the same local network.
- Uses MAC addresses to forward data efficiently.
- Reduces unnecessary network traffic.

### ISP (Internet Service Provider)

- Provides Internet connectivity.
- Assigns a public IP address to the network.
- Routes traffic between users and the Internet.

### Web Server

- Stores website files.
- Processes incoming requests.
- Returns responses to the client.

---

## 💡 Additional Insights

- A domain name and an IP address identify the same destination in different formats—one is human-friendly, the other is machine-friendly.
- DNS lookup happens only when the IP address is not already stored in the cache.
- HTTPS protects data while it is being transmitted but does not hide which website is being visited.
- A webpage is often made up of multiple resources (HTML, CSS, JavaScript, images), so a browser sends multiple requests to fully load a page.
- Different packets belonging to the same request may take different network paths before reaching the destination.

---

## 🧪 Practical Understanding

While studying, I explored how websites identify the correct server even though users type domain names instead of IP addresses.

I also learned that:

- DNS caching helps websites load faster by avoiding repeated DNS lookups.
- Routers forward data between different networks, while switches efficiently deliver data between devices within the same local network.
- Multiple networking components work together in milliseconds to deliver a webpage.

---

## 🛡️ Why This Matters in Cybersecurity

Understanding Internet communication helps security professionals:

- Analyze network traffic.
- Understand how attackers communicate with servers.
- Investigate malicious domains and IP addresses.
- Detect abnormal network behavior.
- Troubleshoot connectivity issues.

---

## ✅ Key Takeaways

- DNS translates domain names into IP addresses.
- Every website request follows a series of networking steps before reaching the server.
- Data is transmitted in packets rather than as a single file.
- HTTPS protects data through encryption.
- Browsers, routers, ISPs, DNS servers, and web servers all play an important role in delivering a webpage.

---

## 💭 Reflection

- Before this lesson, I knew that typing a website address opened a webpage, but I didn't understand the process behind it.
- Learned that opening a website involves multiple networking components working together within seconds.
- I now have a clearer understanding of how DNS, routers, ISPs, packets, and web servers work together.
- This lesson strengthened my networking foundation and will help me understand future topics such as packet analysis, network monitoring, and web security.

---

## 📈 Progress

**Day 5 of 90 ✔️**