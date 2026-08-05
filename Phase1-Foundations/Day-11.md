# 📅 Day 11 – Understanding How the Web Really Works

**Date:** August 03, 2026

---

# 🎯 Objective

The objective of today's lesson was to understand what actually happens behind the scenes when a webpage loads in a browser. Rather than simply thinking of a webpage as something that appears on the screen after clicking a link, I learned that many different processes occur within a few seconds. I explored how browsers work, the difference between the internet and the web, the roles of the front-end and back-end, and how Developer Tools can be used to inspect what is happening beneath the surface.

Today's lesson also introduced me to one of the most important ideas in web security: every webpage consists of hundreds of connections, and each one can become a potential attack surface.

---

# 📖 What I Learned

## 🌐 The Web Is Not the Internet

One of the first things I learned today was that the internet and the web are not the same thing.

The **internet** is the global network that moves data between computers.

The **World Wide Web (WWW)** is a service that runs on top of the internet and allows browsers to display websites using HTML, CSS, and JavaScript.

Before today, I used both terms interchangeably. Now I understand that the internet provides the communication infrastructure, while the web is one of the many services built on top of it.

---

## 🌍 A Browser Is Much More Than a Window

Earlier, I thought browsers like Chrome or Edge simply displayed websites.

Today's lesson showed me that a browser performs many different jobs at the same time.

It acts as:

- 🖥️ A renderer that converts HTML into visible webpages.
- ⚙️ A JavaScript engine that executes interactive code.
- 🌐 A network client that communicates with web servers.
- 💾 A storage system for cookies, cache, and local data.
- 🛡️ A security boundary that controls what websites are allowed to access.

### 💡 My Learning

The **security boundary** was the most interesting concept for me.

I learned that browsers constantly make trust decisions about which scripts can run, which websites can access stored information, and whether one website can interact with another.

I realized that browsers play an important role in protecting users from malicious websites, not just displaying webpages.

---

# ⚡ What Happens When I Press Enter

One of today's biggest lessons was understanding that loading a webpage is actually a sequence of many small events.

The browser performs these steps:

1. DNS Lookup
2. TCP Connection
3. TLS Handshake
4. HTTP Request
5. HTTP Response
6. Resource Fetching
7. Rendering
8. Background Communication

### 💡 My Learning

Earlier, I thought loading a webpage was a single process.

Now I understand that even after a webpage appears on the screen, it continues communicating with multiple servers in the background for analytics, advertisements, updates, and other services.

This helped me understand why cybersecurity professionals analyze network traffic rather than simply looking at the webpage itself.

---

# 🖥️ Front-End vs Back-End

Today's lesson also explained the difference between the two halves of every website.

## 🎨 Front-End

The front-end is everything users can see and interact with.

It includes:

- HTML
- CSS
- JavaScript

This code is downloaded to the browser and can be viewed using **View Page Source**.

---

## 🗄️ Back-End

The back-end is everything that runs on the company's servers.

Examples include:

- Databases
- Customer information
- Authentication systems
- Business logic
- Internal applications

Users never directly see the back-end.

### 💡 My Learning

One important idea I learned was that while many attacks begin through the front-end, the most serious breaches often occur when attackers reach the back-end because that is where valuable organizational data is stored.

---

# 🧩 HTML, CSS and JavaScript

Every webpage is built using three main technologies.

- **HTML** provides the structure.
- **CSS** controls the appearance.
- **JavaScript** adds behavior and interactivity.

### 💡 My Learning

Although I don't need to become a web developer, I now understand why cybersecurity professionals should recognize these technologies.

For example:

- HTML creates forms that attackers can imitate on phishing pages.
- CSS can hide malicious elements.
- JavaScript can modify webpages or execute harmful actions if abused.

This changed how I think about webpages. Instead of seeing only the visible design, I now think about the code running underneath.

---

# 🛠️ Practical Task 1 – Viewing Page Source

## 🌐 Website Chosen

**GitHub**

### 🔍 Findings

While examining the page source, I observed:

- Approximately **30 `<script>` references**
- Third-party services such as:
  - Google
  - Meta
  - Analytics
  - Segment

### 💡 My Learning

Initially, the HTML looked overwhelming because of the large amount of code.

Instead of trying to understand every line, I focused on identifying the overall structure and noticing how many external scripts were being loaded.

This exercise made me realize that modern websites depend on many third-party services beyond the company's own code.

---

# 🛠️ Practical Task 2 – Inspecting Network Activity

For the second task, I opened **Developer Tools** and used the **Network** tab.

At first, I experimented with GitHub, but I found the network activity difficult to understand because many requests were related only to GitHub itself.

To better observe third-party connections, I switched to another website.

## 🌐 Website Chosen

**BBC**

### 🔍 Findings

- **Total Requests:** 264
- **Longest Request:**
  - Domain: `container.com`
  - Type: Document
  - Time: **8.56 seconds**
- **Third-Party Domain:**
  - `cdn.optimizely.com`

### 💡 My Learning

Watching hundreds of requests appear within seconds completely changed my understanding of how webpages load.

I realized that opening one webpage actually involves many different files, including:

- HTML
- CSS
- JavaScript
- Images
- Fonts
- Documents

I also discovered that websites frequently load resources from external domains, which explains why cybersecurity professionals monitor third-party services as carefully as the website itself.

---

# 🎣 Practical Task 3 – Google's Phishing Quiz

The course recommended taking Google's phishing awareness quiz.

Since I had already completed this quiz during **Day 9**, I attempted it again.

### 📊 Result

**Score: 10/10**

### 💡 My Reflection

Unlike my first attempt, every scenario felt much easier to identify.

This showed me that the knowledge gained during previous lessons had already improved my ability to recognize phishing indicators.

Repeating the quiz gave me confidence that consistent practice strengthens security awareness over time.

---

# ⚠️ Challenges I Faced

Today's lesson introduced several new concepts that initially seemed difficult.

When examining website source code, I wasn't sure what information I was supposed to focus on because the page contained thousands of lines of HTML.

Similarly, while inspecting GitHub's Network tab, I struggled to identify third-party domains because most requests appeared to belong to GitHub itself.

After trying a simpler website, I was able to observe external domains much more clearly.

This experience reminded me that choosing an appropriate example is sometimes just as important as understanding the concept itself.

---

# 🛠️ Skills Practiced

- Understanding the difference between the internet and the web
- Exploring Browser Developer Tools
- Viewing webpage source code
- Inspecting live network requests
- Identifying third-party resources
- Understanding front-end and back-end architecture
- Recognizing HTML, CSS, and JavaScript
- Strengthening phishing awareness through repeated practice

---

# ✅ Key Takeaways

- The internet transports data, while the web displays that data through webpages.
- Browsers perform many security-related tasks beyond simply displaying websites.
- Loading a webpage involves multiple networking and security processes rather than a single action.
- Every webpage consists of HTML, CSS, and JavaScript working together.
- Modern websites depend on numerous third-party services and external resources.
- Developer Tools provide valuable insight into how webpages communicate with servers.
- Repeating practical exercises, such as phishing awareness quizzes, demonstrates measurable improvement in cybersecurity knowledge.
- Understanding what happens behind the scenes of a webpage helps develop the mindset needed to analyze web-based attacks.

---

# 💭 Personal Reflection

Today's lesson completely changed the way I look at websites.

Previously, I thought a webpage simply loaded after I clicked a link. Now I understand that what appears on the screen is only the visible result of hundreds of requests, scripts, and background communications happening in just a few seconds.

The biggest realization for me was that cybersecurity is often about understanding what users cannot see. By learning to inspect webpage source code, network requests, and browser activity, I have started looking beyond the interface and focusing on the underlying processes that make the web function.

This shift in perspective has made me more curious about how websites work internally and has helped me think more like someone investigating systems rather than simply using them.