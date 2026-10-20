# Day 23 – Understanding Network Ports 🔌

## 🎯 Objective

Today I learned what network ports are, why a single device can handle many network conversations at the same time, and why open ports are important from a cybersecurity perspective.

The main idea I understood today is:

**IP address identifies the device, while the port identifies the specific service or application involved in the communication.**

---

## 1. 🔌 Understanding Ports

A single laptop can communicate with many different services at the same time. Ports allow the operating system to keep these conversations separate.

I found it useful to think of it like this:

**IP address = building**  
**Port = particular door inside the building**

A port is a 16-bit number, so the available range is **0–65535**.

The three main port ranges are:

- **Well-known ports:** 0–1023
- **Registered ports:** 1024–49151
- **Dynamic/ephemeral ports:** 49152–65535

Some common ports I learned to recognize:

- **22 → SSH**
- **53 → DNS**
- **80 → HTTP**
- **443 → HTTPS**
- **3389 → RDP**
- **5900 → VNC**

---

## 2. 💻 Checking My Own Network Connections with `netstat`

I used the Windows `netstat -an` command to see what network conversations were happening on my laptop.

The output showed:

- Local Address
- Foreign Address
- State

The port number appears after the colon.

For example:

```text
192.168.x.x:49412 → remote-server:443
```

This means my laptop was using local port **49412** to communicate with a remote service on port **443**.

I noticed several established connections using port **443**, which made sense because most modern web traffic uses HTTPS. I also saw connections involving port **80** and port **5228**.

Another interesting part was the **LISTENING** entries. My laptop had services listening on ports such as **135, 445** and several higher Windows service ports.

At first, I thought a LISTENING port automatically meant that the service was exposed to the internet. I learned that this is **not necessarily true**.

For example:

```text
0.0.0.0:445 LISTENING
```

does not by itself prove that the port is reachable from the public internet. Firewall rules, NAT, network configuration and other controls determine whether an outside system can actually reach it.

I also noticed many `127.0.0.1` connections. I learned that **127.0.0.1 refers to my own computer**, so those connections are local to the machine.

---

## 3. 🔎 Understanding Connection States

The `State` column helped me understand what the connections were doing.

- **LISTENING** → A service is waiting for incoming connections.
- **ESTABLISHED** → An active TCP connection exists.
- **TIME_WAIT** → A TCP connection has closed and is being kept temporarily as part of normal TCP cleanup.

This helped me understand that `netstat` is not simply a list of "open ports." It contains different types of network activity that need to be interpreted correctly.

---

## 4. 🌐 Looking at Internet-Exposed Ports with Shodan

I then used Shodan to see the same concept at internet scale.

### 🖥️ RDP — Port 3389

**2,052,793 indexed results**

Top countries at the time of my search:

- China — 557,880
- United States — 395,574
- Singapore — 180,148

### 🖥️ VNC — Port 5900

**387,200 indexed results**

Top countries:

- Singapore — 140,653
- United States — 69,599
- Israel — 35,544

### 🖥️ Telnet — Port 23

**968,924 indexed results**

Top countries:

- China — 328,360
- Brazil — 83,702
- United States — 57,699

The numbers changed when I searched again. This taught me that **Shodan's results are dynamic** and represent what Shodan has currently indexed rather than a permanent count of every device on the internet.

---

## 5. ⚠️ My Most Interesting Finding — Telnet

The Telnet search was the most interesting part of today's practical work.

Some Shodan results displayed service banners containing device information and authentication prompts such as:

```text
User Access Verification
Username:
Password:
```

I did **not** attempt to log in or connect to any of these systems.

The important thing I learned was that an exposed service can reveal useful information simply by responding to a connection. This made the idea of **reconnaissance** much more concrete for me.

---

## 6. 🛡️ Why Open Ports Matter

An open port is **not automatically a vulnerability**.

An open port means something is available to communicate with, so I should be able to answer:

1. Why is this port open?
2. What service is using it?
3. Is that service properly patched?
4. Who actually needs access to it?

I also learned that exposure matters.

A service listening only on **localhost** is different from one accessible on a local network, and that is different again from a service reachable from the public internet.

So the security question is not simply:

> **"Is the port open?"**

It is:

> **"Who can reach this port, and why?"**

---

## 7. 🔗 Connection With Previous Days

Yesterday I learned about IP addresses and NAT. Today I learned that the IP address is only one part of the addressing system.

The simplified picture I now understand is:

**Device → IP address → Port → Service/Application**

For example:

**My laptop → private IP → dynamic source port → HTTPS → remote server port 443**

This helped me understand networking as an actual conversation instead of just memorizing port numbers.

---

## 8. 🧠 What I Learned Personally

The biggest change in my understanding today was realizing that network information has to be interpreted in context.

At first, seeing many LISTENING ports in my `netstat` output looked alarming. After learning more, I understood that a listening service is **not automatically internet-exposed or vulnerable**.

Similarly, seeing a huge number of Shodan results does not mean that all those systems are compromised. It means Shodan has identified systems responding on those ports.

So I learned to distinguish between:

**Open → Exposed → Vulnerable → Compromised**

These are **not the same thing**.

---

## 📝 Conclusion

Today I learned how ports allow one device to maintain many network conversations simultaneously. I used `netstat -an` to examine my own laptop's connections and listening services, and then used Shodan to observe exposed services across the public internet.

The Shodan results made the concept of **attack surface** much more real to me, especially after seeing hundreds of thousands or millions of indexed systems associated with remote-access and legacy services.

Most importantly, I learned that an open port is not automatically a vulnerability. It is a question that needs to be investigated:

**What is running? Why is it accessible? Is it secure? Who needs access?**

That is the mindset I want to carry into the next networking tasks. 🔐
