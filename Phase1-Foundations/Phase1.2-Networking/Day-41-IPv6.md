# Day 41 — IPv6: The Next Generation of Internet Addresses

**MyFirstHack — 90 Days of Cybersecurity**

## 1. Topic

**IPv6 (Internet Protocol version 6)**

Today I learned how IPv6 solves the address limitations of IPv4, how IPv6 addresses are structured and shortened, how IPv4 and IPv6 coexist through dual-stack networking, and what IPv6 means from a cybersecurity perspective.

---

## 2. Why IPv6 Was Needed

IPv4 uses a **32-bit address**, providing approximately **4.3 billion possible addresses**.

As the number of computers, smartphones, servers, IoT devices, and other Internet-connected systems increased, IPv4 addresses became limited.

NAT (Network Address Translation) helped extend the life of IPv4 by allowing multiple private devices to share a public IPv4 address, but it did not solve the fundamental address-space limitation.

IPv6 was designed with a **128-bit address space**, providing approximately:

**340 undecillion possible addresses**

This provides an enormous number of unique addresses for Internet-connected devices.

### Basic comparison

| Feature | IPv4 | IPv6 |
|---|---|---|
| Address size | 32-bit | 128-bit |
| Format | Decimal | Hexadecimal |
| Example | `192.168.1.1` | `2001:db8::1` |
| Address space | ~4.3 billion | ~340 undecillion |
| NAT for address conservation | Common | Generally unnecessary |

---

## 3. IPv6 Address Structure

An IPv6 address contains **8 groups** of hexadecimal digits separated by colons.

Example:

```text
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

Each group contains up to **4 hexadecimal digits**.

Hexadecimal uses:

```text
0–9
A–F
```

IPv6 therefore looks very different from the familiar IPv4 format.

---

## 4. IPv6 Address Shortening

IPv6 addresses can often be written in a shorter form.

There are two important rules.

### Rule 1 — Remove leading zeros

For example:

```text
0db8 → db8
0042 → 42
0370 → 370
0000 → 0
```

### Rule 2 — Replace consecutive zero groups with `::`

Example:

```text
2001:0db8:0000:0000:0000:ff00:0042:8329
```

After removing leading zeros:

```text
2001:db8:0:0:0:ff00:42:8329
```

The three consecutive zero groups can then be replaced with `::`:

```text
2001:db8::ff00:42:8329
```

### Important rule

`::` can be used **only once** in an IPv6 address because it represents one or more consecutive groups of zeros.

---

## 5. Important IPv6 Address Types

### Loopback — `::1`

`::1` is the IPv6 loopback address.

It refers back to the local device itself.

It is similar in concept to IPv4:

```text
127.0.0.1
```

---

### Link-local — `fe80::/10`

IPv6 devices can automatically have link-local addresses.

They are used for communication on the local network link.

A common example begins with:

```text
fe80::
```

---

### Global IPv6 Address

A global IPv6 address can be used for communication across networks and the Internet, subject to routing and firewall rules.

A device may have multiple IPv6 addresses at the same time.

---

## 6. Dual-Stack Networking

IPv4 has not simply disappeared because IPv6 was introduced.

The Internet is going through a gradual transition, and many modern devices and networks support **both IPv4 and IPv6**.

This is called **dual stack**.

Conceptually:

```text
                 Internet
                /        \
             IPv4        IPv6
               \          /
                \        /
                  Device
```

A device can use IPv4 when communicating with an IPv4 destination and IPv6 when communicating with an IPv6 destination, depending on network and destination support.

### Important point

**IPv4 and IPv6 being enabled does not mean both are used for every connection.**

---

## 7. Why Both Protocols Are Commonly Enabled

The transition from IPv4 to IPv6 cannot happen instantly.

There are still:

- IPv4-only systems
- IPv6-capable systems
- Dual-stack networks
- Legacy applications and infrastructure

Therefore, modern operating systems commonly support IPv4 and IPv6 together.

This allows devices to communicate during the transition period.

---

## 8. IPv6 and NAT

NAT became extremely common with IPv4 because public IPv4 addresses are limited.

With IPv6's huge address space, NAT is generally not required for address conservation.

This creates an important security lesson.

### NAT is not a firewall.

NAT often made unsolicited inbound connections more difficult as a side effect, but that should not be confused with deliberate security protection.

In IPv6, security should be intentionally provided through controls such as:

- Firewalls
- Access-control rules
- Network monitoring
- IDS/IPS
- Logging
- SIEM visibility

---

## 9. IPv6 Security Mindset

The main security lesson from today's topic is:

> **Security should be deliberate, not accidental.**

An organization should not assume that IPv6 is safe simply because its IPv4 network is secured.

For example:

```text
IPv4 → Firewall → Monitoring → Logs → SIEM
                         ✓
```

But if IPv6 is running without the same visibility:

```text
IPv6 → No monitoring
              ↓
       Security blind spot
```

An attacker could potentially use an overlooked IPv6 path if security controls are not properly configured.

Therefore, IPv6 traffic should be:

- Controlled by appropriate firewall rules
- Monitored
- Logged
- Included in security investigations
- Visible to security monitoring/SIEM systems

---

## 10. SLAAC

**SLAAC** stands for **Stateless Address Autoconfiguration**.

It allows IPv6 devices to configure addresses automatically using information provided by IPv6 routers.

This makes IPv6 network configuration easier.

IPv6 networks can also use **DHCPv6**, depending on how the network is designed.

---

## 11. IPv6 Privacy

Some older IPv6 addressing approaches could expose identifiers associated with a network interface.

This raised privacy and tracking concerns.

Modern operating systems can use **temporary/privacy IPv6 addresses** that change over time, helping reduce long-term tracking based solely on a stable address.

---

## 12. Why the IPv6 Transition Is Slow

IPv4 and IPv6 are not directly compatible at the protocol level.

The Internet therefore cannot simply switch from IPv4 to IPv6 in one day.

The transition can involve:

- **Dual stack** — running IPv4 and IPv6 together
- **Translation** — translating between IPv4 and IPv6
- **Tunneling** — carrying one protocol through another network

IPv4 also survived longer than originally expected because NAT and other techniques reduced the immediate pressure caused by IPv4 address exhaustion.

---

# 13. Practical Lab

As part of today's learning, I attempted to check IPv6 on my own connection.

### Step 1 — Finding IPv6 addresses

I used the Windows command:

```text
ipconfig
```

The goal was to identify:

- IPv4 address
- Link-local IPv6 address
- Global IPv6 address, if available

I did not find an IPv6 address in the output I checked.

---

### Step 2 — Testing IPv6 Connectivity

I used **test-ipv6.com** to check whether my connection could communicate using IPv6.

The test reported that my IP addresses could not be detected because of interference from a browser add-on/filter.

It also reported that a firewall or browser filter was preventing critical tests from running.

The readiness score was:

```text
N/A
```

Therefore, this result could **not conclusively determine the actual IPv6 capability of my connection** because the test itself was being blocked.

---

### Step 3 — Checking Public IPv6

I also checked my connection using whatismyipaddress.com.

The result showed:

```text
IPv6: Not detected
```

This suggests that a public IPv6 address was not detected by that service at the time of testing.

However, because the IPv6 connectivity test was also affected by browser filtering, I should not treat this alone as proof that my network completely lacks IPv6 support.

---

## 14. Practice IPv6 Address

The address provided for practice was:

```text
2001:0db8:0000:0000:0000:ff00:0042:8329
```

After removing leading zeros:

```text
2001:db8:0:0:0:ff00:42:8329
```

After replacing the consecutive zero groups:

```text
2001:db8::ff00:42:8329
```

### Final shortened address

**`2001:db8::ff00:42:8329`**

---

# 15. Security Implication

IPv6 changes the security mindset because we cannot depend on NAT's side effects to provide protection.

The **firewall** should deliberately decide which inbound traffic is allowed and which is blocked.

If an organization secures and monitors IPv4 but leaves IPv6 unmonitored, IPv6 could become an overlooked path.

Therefore:

> **Don't secure IPv4 and forget IPv6.**

Both protocols need appropriate security controls and visibility.

---

# 16. Connection With Previous Learning

Today's topic connects with several concepts I learned previously.

### Day 37 — SIEM

If IPv6 security events are not sent to the SIEM, the SIEM cannot correlate or alert on them.

### Day 38 — Logs

If IPv6 activity isn't properly logged, investigating an incident becomes much harder.

### Day 40 — Zero Trust

Zero Trust teaches us not to assume that something is safe simply because it is inside the environment.

### Day 41 — IPv6

The same principle applies to network protocols:

> **Know what is running, monitor it, and deliberately control it.**

---

# 17. Key Takeaways

- IPv4 uses **32-bit** addresses.
- IPv6 uses **128-bit** addresses.
- IPv6 provides an enormous address space.
- IPv6 addresses use hexadecimal and colons.
- Leading zeros can be removed.
- Consecutive zero groups can be replaced with `::`.
- `::1` is the IPv6 loopback address.
- `fe80::/10` is the IPv6 link-local range.
- Modern devices commonly support both IPv4 and IPv6.
- Running both protocols is called **dual stack**.
- IPv6 does not require NAT for address conservation.
- NAT should not be considered a firewall.
- IPv6 security must be deliberate.
- IPv6 should be included in firewall policies, monitoring, logging, and SIEM visibility.
- An unmonitored IPv6 path can become a security blind spot.
- The transition from IPv4 to IPv6 is gradual because the two protocols are not directly compatible.

---

## Final Reflection

Today's learning helped me understand that IPv6 is not simply about creating more IP addresses.

It also changes how network security needs to be approached.

The biggest lesson I took from Day 41 is:

> **A network can have more than one path, and securing only the path we normally look at is not enough.**

IPv6 may run alongside IPv4, so cybersecurity professionals need to understand, monitor, and secure both.