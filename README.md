<div align="center">

# Secure Coding for Web Applications

### Student Lab Pack

**A hands-on workshop teaching web application security fundamentals**

*Workshop at Srinakharinwirot University · Salozz*

![Date](https://img.shields.io/badge/Date-March%2016%2C%20206-blue)
![Labs](https://img.shields.io/badge/Labs-6-green)
![Vulnerabilities](https://img.shields.io/badge/Vulnerabilities-5-red)
![Difficulty](https://img.shields.io/badge/Difficulty-Beginner-yellow)

**https://salozz-secureweb-workshop-mar26.netlify.app/**

</div>

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Topics Covered](#-topics-covered)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Lab Details](#-lab-details)
  - [Lab 1A: XSS](#lab-1a--cross-site-scripting-xss)
  - [Lab 1B: SQL Injection](#lab-1b--sql-injection)
  - [Lab 2A: CSRF](#lab-2a--cross-site-request-forgery-csrf)
  - [Lab 2B: Authentication](#lab-2b--authentication-patterns)
  - [Lab 2C: Security Headers](#lab-2c--http-security-headers)
  - [Lab 3: Deployment](#lab-3--deploy-securely)
  - [Challenge Round](#-challenge-round--secure-code-review)
- [Quick Reference](#-quick-reference)
- [Resources](#-resources)
- [License](#-license)

---

## 🎯 Overview

This repository contains interactive HTML labs for learning common web security vulnerabilities and defenses. Each lab demonstrates a vulnerability, explains how the attack works, and guides students through fixing the issue.

> **✨ All labs run entirely in the browser — no backend setup required!**

---

## 📚 Topics Covered

| # | Vulnerability | Severity | Lab |
|---|---------------|----------|-----|
| 1 | Cross-Site Scripting (XSS) | 🔴 High | Lab 1A |
| 2 | SQL Injection | 🔴 Critical | Lab 1B |
| 3 | Cross-Site Request Forgery (CSRF) | 🟠 Medium | Lab 2A |
| 4 | Authentication Design Flaws | 🔴 High | Lab 2B |
| 5 | Security Misconfiguration | 🟡 Medium | Lab 2C |

---

## 📁 Repository Structure

```
lab_materials/
├── 📄 index.html                # Workshop landing page
│
├── 📂 lab1a/
│   ├── index.html               # XSS vulnerable demo
│   └── index_secure.html        # XSS patched version
│
├── 📂 lab1b/
│   └── login.html               # SQL Injection demo
│
├── 📂 lab2a/
│   └── csrf_demo.html           # CSRF simulation
│
├── 📂 lab2b/
│   └── auth_patterns.html       # Authentication patterns
│
├── 📂 lab2c/
│   ├── headers_guide.html       # HTTP security headers guide
│   └── _headers                 # Netlify security headers file
│
├── 📂 lab3/
│   └── deployment_guide.html    # GitHub + Netlify deployment
│
├── 📂 challenge/
│   └── challenge.html           # Secure code review challenge
│
└── 📄 README.md
```

---

## 🚀 Getting Started

1. **Clone or download** this repository
2. **Open `index.html`** in your web browser
3. **Follow the labs in order:** 1A → 1B → 2A → 2B → 2C → 3
4. **Complete the challenge** to test your knowledge

---

## 🧪 Lab Details

### Lab 1A — Cross-Site Scripting (XSS)

> **File:** [`lab1a/index.html`](lab1a/index.html)

A simple comment board that contains a reflected XSS vulnerability.

**What you'll learn:**
- How attackers inject malicious JavaScript
- Why `innerHTML` is dangerous
- How to use safe DOM methods

**Attack Payload:**
```html
<img src=x onerror="alert('XSS! Cookie: ' + document.cookie)">
```

**The Fix:**
```javascript
// ❌ Vulnerable
element.innerHTML += input;

// ✅ Secure
element.textContent = input;
```

---

### Lab 1B — SQL Injection

> **File:** [`lab1b/login.html`](lab1b/login.html)

A login form demonstrates how building SQL queries directly from user input can lead to authentication bypass.

**What you'll learn:**
- How SQL injection manipulates query logic
- How to observe attacks via DevTools console
- Why parameterized queries are essential

**Attack Payload:**
```sql
admin' OR '1'='1' --
```

**The Fix:**
```javascript
// ❌ Vulnerable
const query = `SELECT * FROM users WHERE username='${username}'`;

// ✅ Secure
const query = 'SELECT * FROM users WHERE username = ?';
db.execute(query, [username]);
```

---

### Lab 2A — Cross-Site Request Forgery (CSRF)

> **File:** [`lab2a/csrf_demo.html`](lab2a/csrf_demo.html)

A simulated banking interface demonstrates how attackers can trick browsers into making unintended requests.

**What you'll learn:**
- How browsers automatically send cookies
- How hidden forms trigger malicious actions
- Why CSRF tokens are necessary

**Attack Simulation:**
```html
<form action="bank.com/transfer" method="POST" style="display:none">
  <input name="to" value="hacker">
  <input name="amount" value="1000">
</form>
<script>document.getElementById('attack').submit();</script>
```

**The Fix:**
```html
<input type="hidden" name="csrf_token" value="random_token_here">
```

---

### Lab 2B — Authentication Patterns

> **File:** [`lab2b/auth_patterns.html`](lab2b/auth_patterns.html)

Compare good and bad authentication practices.

**What you'll learn:**

| Practice | ❌ Bad | ✅ Good |
|----------|--------|---------|
| Password Storage | Plaintext, MD5 | bcrypt, Argon2 |
| Token Generation | `Math.random()` | `crypto.randomBytes()` |
| Cookie Flags | None | HttpOnly, Secure, SameSite |

---

### Lab 2C — HTTP Security Headers

> **File:** [`lab2c/headers_guide.html`](lab2c/headers_guide.html)

Configure security headers for production deployment.

**Essential Headers:**
```
Content-Security-Policy: default-src 'self'
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Strict-Transport-Security: max-age=31536000
Referrer-Policy: no-referrer
Permissions-Policy: camera=(), microphone=()
```

**Verification:** Test your site at [securityheaders.com](https://securityheaders.com) — target **A+** grade!

---

### Lab 3 — Deploy Securely

> **File:** [`lab3/deployment_guide.html`](lab3/deployment_guide.html)

Deploy your secure application to the internet.

**Steps:**
1. Initialize Git repository
2. Commit project files
3. Push to GitHub
4. Deploy via Netlify
5. Verify security headers score

---

### 🏆 Challenge Round — Secure Code Review

> **File:** [`challenge/challenge.html`](challenge/challenge.html)

Inspect a vulnerable application and identify security flaws.

**Find issues like:**
- 🔓 Credentials sent via GET
- 🎲 Insecure session tokens
- 🍪 Missing cookie flags
- 🕵️ Client-side authentication
- 💉 Unsafe input handling

---

## ⚡ Quick Reference

### Vulnerability Fixes at a Glance

| Vulnerability | Root Cause | Fix |
|---------------|------------|-----|
| **XSS** | User input rendered as HTML | Use `textContent` + CSP |
| **SQL Injection** | String concatenation in queries | Use parameterized queries |
| **CSRF** | No request validation | Add CSRF tokens + SameSite |
| **Weak Auth** | Poor hashing, predictable tokens | bcrypt + CSPRNG + secure cookies |
| **Missing Headers** | Default server config | Add security headers |

---

## 🔗 Resources

| Resource | Description |
|----------|-------------|
| [![OWASP](https://img.shields.io/badge/OWASP-Top%2010-blue)](https://owasp.org/www-project-top-ten/) | Industry-standard vulnerability list |
| [![PortSwigger](https://img.shields.io/badge/PortSwigger-Academy-orange)](https://portswigger.net/web-security) | Free interactive security labs |
| [![securityheaders](https://img.shields.io/badge/securityheaders.com-Scan-green)](https://securityheaders.com) | Test your security headers |
| [![TryHackMe](https://img.shields.io/badge/TryHackMe-Learn-red)](https://tryhackme.com) | Gamified cybersecurity training |
| [![MDN](https://img.shields.io/badge/MDN-Web%20Security-blue)](https://developer.mozilla.org/en-US/docs/Web/Security) | Browser security documentation |

---

## 📜 License

Educational use permitted. Feel free to use and modify for teaching purposes.

---

<div align="center">

**Made with ❤️ for Secure Coding Workshop**

*Secure Coding for Web Applications · Srinakharinwirot University · Salozz*

</div>
