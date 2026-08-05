# 🍪 Day 13 – Understanding Web Cookies

## 📚 What I Learned Today

- Learned what **cookies** are and why websites use them.
- Understood that a cookie is a **small text file** stored in the browser.
- Learned that cookies allow websites to **remember users** between different page requests.
- Before today, I thought cookies were mainly used for advertisements and tracking. Now I understand they are an essential part of web authentication.
- Learned that the web is **stateless**, meaning every HTTP request is treated as a completely new request.
- Understood that without cookies:
  - Websites would not remember logged-in users.
  - Users would have to log in again on every page.
  - Shopping carts would not work.
  - Personalized experiences would not be possible.

---

# 🌐 Why Cookies Exist

- HTTP is a **stateless protocol**.
- Every request sent by the browser is independent.
- The server has no memory of previous requests.
- Cookies solve this problem by giving the web "memory."
- The server sends a cookie to the browser after authentication.
- The browser stores the cookie.
- Every future request automatically includes the cookie.
- The server recognizes the session using the cookie instead of asking for credentials repeatedly.

---

# 🍪 Cookie Structure

A cookie usually contains:

- **Name**
- **Value**
- **Expiry Date / Max-Age**
- **Security Flags**

### Example

```text
session_id=a8f3kp29d1xq7b4m
```

### My Learning

- The **Name** identifies the cookie.
- The **Value** is usually a long random string.
- The cookie value is **not my password**.
- The server stores the actual user information.
- The cookie acts as a unique session identifier.
- The browser simply stores and returns the cookie whenever required.

---

# 🔑 Session Cookies

Today I learned that the most important cookie is the **Session Cookie**.

## What a Session Cookie Does

- Proves that I have already logged in.
- Identifies me as an authenticated user.
- Allows me to move between pages without logging in repeatedly.
- Keeps me logged in until the session expires or I log out.

## Important Observations

- The server checks the session cookie on every request.
- My password is **not** sent with every request.
- Whoever possesses a valid session cookie is treated as the logged-in user.
- Session cookies can bypass passwords because authentication has already happened.

---

# 🔥 Firesheep Attack

## What I Learned

- Firesheep was released in **2010**.
- It captured session cookies over public Wi-Fi.
- Websites only encrypted the login page.
- The remaining session travelled over HTTP.
- Attackers could steal cookies and log into other people's accounts without passwords.

## Impact

- Major websites adopted HTTPS for the entire browsing session.
- HTTPS became the modern web standard.
- Public Wi-Fi became much safer than before.

---

# 🛡️ Cookie Security Flags

## 🔒 Secure

- Cookie is sent only over HTTPS.
- Prevents cookies from travelling through HTTP.

## 🚫 HttpOnly

- Prevents JavaScript from accessing cookies.
- Protects against Cross-Site Scripting (XSS).

## 🌍 SameSite

- Controls when cookies are sent from other websites.
- Protects against Cross-Site Request Forgery (CSRF).

## ⏳ Expires / Max-Age

- Determines how long the cookie remains valid.
- Short-lived cookies reduce the impact of stolen sessions.

---

# 💻 Practical Task 1 – Inspecting Cookies

## Website

- GitHub

## Findings

- **Total Cookies:** 12
- **Session-related Cookies:**
  - `user_session`
  - `logged_in`

## Security Flags Observed

### user_session

- ✅ Secure
- ✅ HttpOnly
- ✅ SameSite = Lax

## My Learning

- GitHub follows good security practices.
- Session cookies are protected using multiple security flags.
- Websites remember users through cookies rather than passwords.
- This was my first time viewing the actual cookies stored by my browser.

---

# 🌐 Practical Task 2 – Watching a Cookie Travel

## Website

- GitHub

## Findings

- Observed **Set-Cookie** in the **Response Headers** after login.
- Observed the same cookie inside the **Cookie Request Header** in later requests.
- Security flags found:
  - Secure
  - HttpOnly
  - SameSite = Lax

## My Learning

- The server creates a session after successful login.
- The browser automatically stores the session cookie.
- Every future request automatically includes that cookie.
- The browser handles this process without requiring user interaction.

---

# 🧪 Practical Task 3 – Breaking a Session Cookie

## Website

- Reddit

## Session Cookie Edited

- `reddit_session`

## Action Performed

- Changed one character in the cookie value.

## Result

- Reddit immediately logged me out.
- Redirected me to the login page.
- The server rejected the modified cookie.
- Logging in again generated a new valid session cookie.

## My Learning

- A session cookie is the real proof of identity after login.
- Changing a single character invalidated the session.
- My password remained unchanged.
- The server treated me as a completely new user.
- This demonstrated why attackers try to steal valid session cookies instead of passwords.

---

# 💡 Important Concepts Learned

- Cookies are **not passwords**.
- Cookies are **not user accounts**.
- Cookies store a session identifier.
- The actual user information is stored on the server.
- Session cookies act like a digital identity card.
- HTTPS protects cookies while they travel across the internet.
- HTTPS cannot protect cookies if they are stolen from the browser.
- Cookie security flags make cookie theft much more difficult.
- Session hijacking is one of the most dangerous web attacks.
- A stolen session cookie can allow attackers to bypass passwords and Multi-Factor Authentication (MFA).

---

# ✅ Key Takeaways

- Learned why cookies are essential for modern websites.
- Understood why the web needs cookies because HTTP is stateless.
- Learned how websites remember logged-in users.
- Understood the structure of a cookie.
- Learned the difference between normal cookies and session cookies.
- Learned why session cookies are valuable to attackers.
- Understood how Firesheep changed web security.
- Learned the purpose of the **Secure**, **HttpOnly**, **SameSite**, and **Expires** flags.
- Successfully inspected real cookies stored by GitHub.
- Successfully observed the **Set-Cookie** and **Cookie** headers in Developer Tools.
- Successfully edited my own Reddit session cookie and observed the session being invalidated.
- Gained a practical understanding of how authentication works behind the scenes.
- Realized that a small text string stored in the browser determines whether a website recognizes me as a logged-in user or a complete stranger.

---

# 📝 Personal Reflection

Before today's lesson, I thought cookies were mostly related to advertisements and tracking. After completing both the theory and practical exercises, I now understand that cookies are one of the most important parts of web authentication.

The hands-on activities made today's concepts much easier to understand. Watching a cookie being created, seeing it travel between the server and browser, and intentionally breaking a session cookie helped me understand how websites identify users.

This was one of the most practical lessons so far because I was able to observe how authentication works behind the scenes instead of only reading about it.