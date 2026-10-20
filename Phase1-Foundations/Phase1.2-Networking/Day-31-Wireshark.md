# Day 31 — Wireshark: Making Network Traffic Visible

## 📅 MyFirstHack — 90 Days of Cybersecurity

---

## 🔍 Overview

Today I learned how to use **Wireshark**, a network packet analyzer that captures and displays real network traffic.

For the past several days, I had been learning networking concepts such as:

- OSI model
- IP addresses
- MAC addresses
- Ports
- DNS
- TCP
- UDP
- ARP

Wireshark allowed me to see these concepts happening in real network traffic instead of only learning them theoretically.

The main goal of today's learning was to capture traffic from my own machine and understand what individual packets contain.

---

## 🧠 What is Wireshark?

**Wireshark** is a free and open-source network packet analyzer.

It captures packets passing through a selected network interface and allows them to be inspected in detail.

Wireshark is commonly used for:

- Network troubleshooting
- Protocol analysis
- Security investigations
- Traffic analysis
- Network debugging
- Learning how network protocols work

Wireshark does not normally interfere with the communication. It captures and analyzes copies of packets passing through the network interface.

---

## 📦 What is a Packet?

A packet is a unit of data transmitted across a network.

When devices communicate, information is divided into packets and sent between the source and destination.

Wireshark captures these packets and allows me to inspect:

- Source
- Destination
- Protocol
- Ports
- Headers
- Flags
- Packet contents
- Raw bytes

---

# 🖥️ The Three Wireshark Panes

Wireshark displays captured packets using three main panes.

## 1. Packet List Pane

The packet list is the top pane.

It provides an overview of all captured packets.

It can show:

- Packet number
- Timestamp
- Source
- Destination
- Protocol
- Length
- Information

Example:

```text
No.    Source        Destination       Protocol
1      Laptop        DNS Server        DNS
2      DNS Server    Laptop            DNS
3      Laptop        Server            TCP
```

The packet list helps me quickly identify the packets I want to investigate.

---

## 2. Packet Details Pane

The packet details pane is the middle pane.

When I select a packet, Wireshark breaks it down into different protocol layers.

For example:

```text
Frame
 └── Ethernet
      └── IPv4
           └── TCP
                └── TLS / Application
```

This connects directly with the OSI model I learned earlier.

I can expand each section to inspect individual fields.

---

## 3. Packet Bytes Pane

The packet bytes pane is the bottom pane.

It displays the raw packet data as:

- Hexadecimal
- ASCII

The bytes shown here represent the actual data contained in the packet.

I normally don't need to manually interpret every byte because Wireshark decodes the protocols and displays understandable information in the packet details pane.

---

# 🔎 Wireshark Display Filters

A normal capture can contain thousands of packets.

Filtering is therefore one of the most important Wireshark skills.

A display filter allows me to show only the packets that I am interested in.

## Filter by Protocol

### DNS

```text
dns
```

Shows DNS traffic.

### TCP

```text
tcp
```

Shows TCP traffic.

### UDP

```text
udp
```

Shows UDP traffic.

### ARP

```text
arp
```

Shows ARP traffic.

---

## Filter by IP Address

```text
ip.addr == 8.8.8.8
```

This shows traffic to or from the specified IP address.

---

## Filter by TCP Port

```text
tcp.port == 443
```

This shows TCP traffic involving port 443.

---

## Filter by UDP Port

```text
udp.port == 53
```

This shows UDP traffic involving port 53.

---

## Combining Filters

The `&&` operator means **AND**.

```text
dns && ip.addr == 192.168.1.1
```

The `||` operator means **OR**.

```text
dns || arp
```

Filtering makes it much easier to find specific conversations inside a large packet capture.

---

# 🌐 DNS Traffic

During my practical, I captured a DNS lookup for:

```text
example.com
```

I used the display filter:

```text
dns
```

I found both the DNS query and the DNS response.

The response contained two IPv4 addresses:

```text
104.20.23.154
172.66.147.243
```

The DNS process looked like:

```text
My Computer
     |
     | DNS Query
     | "What is the IP address of example.com?"
     v
DNS Server
     |
     | DNS Response
     v
104.20.23.154
172.66.147.243
```

This allowed me to see the DNS mechanism I had previously learned about in an actual packet capture.

---

# 🤝 TCP Three-Way Handshake

I also captured a complete TCP three-way handshake.

The three steps were:

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
```

My capture showed:

```text
TCP 64237 → 443    [SYN]

TCP 443 → 64237    [SYN, ACK]

TCP 64237 → 443    [ACK]
```

The connection was using destination port:

```text
443
```

The client was using temporary source port:

```text
64237
```

This demonstrated the TCP connection establishment process in real traffic.

---

# 🚪 Understanding Ports Through Wireshark

Wireshark allowed me to see source and destination ports inside TCP packets.

For example:

```text
Source Port:      64237
Destination Port: 443
```

This helped me understand that ports are not just numbers to memorize.

They identify the services involved in network communication.

---

# 🧱 Exploring the Network Layers

I selected a packet and expanded its different sections.

I observed:

```text
Ethernet
   ↓
IPv4
   ↓
TCP
   ↓
TLS / Application
```

## Ethernet

The Ethernet section showed:

- Source MAC address
- Destination MAC address
- Ethernet type

The captured packet showed:

```text
Source MAC:      c4:75:ab:3c:f2:71
Destination MAC: f2:0e:fb:59:90:c1
Type:            IPv4
```

## IPv4

The IPv4 section showed:

```text
Source IP:      10.94.190.131
Destination IP: 142.250.182.206
```

This connected the packet to the IP addressing concepts I had learned previously.

## TCP

The TCP section showed:

- Source port
- Destination port
- TCP flags
- Other TCP information

For the handshake, I observed the SYN, SYN-ACK, and ACK flags.

---

# 📡 Protocols Observed

During the capture, I observed the following protocols:

## TCP

TCP provides reliable, connection-oriented communication.

I observed a TCP three-way handshake using:

```text
SYN → SYN-ACK → ACK
```

## UDP

UDP provides connectionless communication without the TCP three-way handshake.

## DNS

DNS is used to translate domain names into IP addresses.

I observed a DNS query and response for `example.com`.

## TLS 1.2

I observed TLS 1.2 encrypted traffic.

## TLS 1.3

I also observed TLS 1.3 encrypted traffic.

## ARP

ARP is used on local networks to help determine the MAC address associated with an IP address.

I did not expect to see ARP during normal browsing, which made it an interesting part of the capture.

---

# 🔐 HTTPS and TLS

I observed encrypted TLS traffic during the capture.

Wireshark can still show useful metadata about encrypted communication, such as:

- Source
- Destination
- Ports
- TLS version
- Timing
- Packet sizes
- Connection information

However, the actual encrypted application data is not simply displayed as readable website content.

A useful analogy is:

> Wireshark can see the envelope, but not necessarily the letter inside.

This demonstrated why encryption protects the contents of network communication while some metadata remains visible.

---

# 🛡️ Responsible Packet Capture

Packet capture should only be performed where I have authorization.

## Safe environments

- My own computer
- My own network
- Authorized networks
- Cybersecurity labs
- Systems where I have explicit permission

## Unsafe or unauthorized situations

I should not use Wireshark to capture or inspect other people's private traffic without permission.

I should also not capture traffic on a corporate or institutional network unless I am explicitly authorized to do so.

The important cybersecurity principle is:

> **Technical ability does not equal authorization.**

---

# 🧪 Practical Lab

## Step 1 — Select Network Interface

I selected my active:

```text
Wi-Fi
```

interface in Wireshark.

---

## Step 2 — Capture Traffic

I started a live capture and allowed Wireshark to record network traffic from my own machine.

---

## Step 3 — Generate Traffic

While the capture was running, I:

1. Opened a web browser.
2. Visited `example.com`.
3. Visited another normal website.
4. Returned to Wireshark.
5. Stopped the capture.

---

## Step 4 — Find DNS Traffic

I used:

```text
dns
```

to filter the capture.

I found the DNS query and response for:

```text
example.com
```

The response returned:

```text
104.20.23.154
172.66.147.243
```

---

## Step 5 — Find TCP Handshake

I used:

```text
tcp.flags.syn == 1
```

to find TCP SYN packets.

I identified:

```text
TCP 64237 → 443    [SYN]
TCP 443 → 64237    [SYN, ACK]
TCP 64237 → 443    [ACK]
```

This confirmed a complete TCP three-way handshake.

---

## Step 6 — Explore Packet Layers

I selected a packet and expanded:

```text
Ethernet
IPv4
TCP
TLS / Application
```

I was able to see MAC addresses, IP addresses, ports, TCP flags, and protocol information inside a real packet.

---

# 📊 Capture Observation

My capture reached approximately:

```text
3,469 packets
```

This was a short practical session involving only a few intentional actions.

The large number of packets showed me that a connected computer communicates constantly with networks and online services.

Some traffic was generated by my browsing, while other traffic was background communication.

This was an important practical observation because I could see how active a connected computer can be even when I am not intentionally sending network requests.

---

# 💡 Key Learnings

Today I learned:

1. Wireshark captures and analyzes network packets.
2. A packet can be inspected layer by layer.
3. Wireshark has three main panes: packet list, packet details, and packet bytes.
4. Display filters make large captures easier to analyze.
5. DNS queries and responses can be observed directly.
6. TCP's SYN → SYN-ACK → ACK handshake can be captured in real traffic.
7. Source and destination ports can be inspected in packets.
8. Ethernet frames contain MAC addresses.
9. IPv4 packets contain source and destination IP addresses.
10. TLS traffic can be observed even though its application data is encrypted.
11. ARP, TCP, UDP, DNS, TLS 1.2, and TLS 1.3 can appear during normal network activity.
12. A computer can generate thousands of packets during a short period.
13. Packet capture should only be performed on systems and networks where I have authorization.

---

# 🔗 Connection With Previous Learning

Wireshark connected many previous networking concepts together:

```text
OSI Model
     ↓
Ethernet / IP / TCP / Application
     ↓
IP Addresses
     ↓
Source and Destination IPs
     ↓
Ports
     ↓
TCP / UDP
     ↓
DNS
     ↓
TCP Handshake
     ↓
Wireshark
     ↓
Real Network Traffic
```

Previously, these concepts were individual topics.

Wireshark allowed me to see them working together in real network communication.

---

# 🎯 Final Takeaway

The biggest lesson from today was:

> **Wireshark turns networking theory into something visible, searchable, and analyzable.**

Instead of only learning how DNS, TCP, ports, IP addresses, and the OSI model work, I was able to capture real packets and identify those concepts myself.

Today networking became much less abstract.

I can now look at network traffic and begin to recognize **what is happening, which protocols are involved, where the traffic is going, and how the communication is structured.**

---

## ✅ Day 31 Status

**Wireshark practical completed successfully.**

### Completed:

- Installed and opened Wireshark
- Captured live traffic
- Used the Wi-Fi interface
- Filtered DNS traffic
- Found `example.com` DNS query and response
- Identified returned IPv4 addresses
- Captured a TCP three-way handshake
- Identified port 443
- Explored Ethernet and IPv4 layers
- Examined TCP ports and flags
- Observed TCP, UDP, DNS, TLS 1.2, TLS 1.3, and ARP
- Observed approximately 3,469 packets
- Practiced responsible packet capture

**Day 31 complete. 🚀**