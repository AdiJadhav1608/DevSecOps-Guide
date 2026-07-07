# 🌐 Common Web Attacks

---

# 📖 Introduction

Web applications are one of the most common targets for cyberattacks because they are accessible over the internet and often handle sensitive data such as user credentials, financial information, and personal records.

A **Web Attack** is any malicious attempt to exploit vulnerabilities in a web application, server, or API to gain unauthorized access, steal data, disrupt services, or compromise system security.

Understanding common web attacks is essential for developers, DevOps engineers, and security professionals to build secure applications and implement effective security controls.

> **"You can't defend against an attack if you don't understand how it works."**

---

# 🎯 Objectives

By learning about common web attacks, you will be able to:

- Understand how attackers exploit web applications.
- Identify common web vulnerabilities.
- Learn prevention techniques.
- Build secure applications.
- Strengthen DevSecOps pipelines with security testing.

---

# 🏗️ Common Web Attacks

The most common web attacks include:

1. SQL Injection (SQLi)
2. Cross-Site Scripting (XSS)
3. Cross-Site Request Forgery (CSRF)
4. Command Injection
5. File Inclusion
6. Directory Traversal
7. Server-Side Request Forgery (SSRF)
8. XML External Entity (XXE)
9. Clickjacking
10. Brute Force Attack

---

# 💉 1. SQL Injection (SQLi)

## 📖 What is SQL Injection?

SQL Injection occurs when an attacker inserts malicious SQL commands into application input fields to manipulate the backend database.

---

## Example

User Login Query

```sql
SELECT * FROM users
WHERE username='admin'
AND password='12345';
```

Attacker Input

```text
Username: admin' --
Password: anything
```

Resulting Query

```sql
SELECT * FROM users
WHERE username='admin' --'
AND password='anything';
```

The password check is ignored, allowing unauthorized access.

---

## Impact

- Database compromise
- Data theft
- Data modification
- Data deletion
- Authentication bypass

---

## Prevention

- Use Prepared Statements
- Parameterized Queries
- Validate user input
- Least Privilege Database Access

---

# 🖥️ 2. Cross-Site Scripting (XSS)

## 📖 What is XSS?

Cross-Site Scripting occurs when attackers inject malicious JavaScript into web pages viewed by other users.

---

## Example

```html
<script>
alert("You are hacked!");
</script>
```

If input is not sanitized, the script executes in another user's browser.

---

## Impact

- Cookie theft
- Session hijacking
- Fake login pages
- Account takeover

---

## Prevention

- Validate user input
- Escape HTML output
- Use Content Security Policy (CSP)
- Sanitize user data

---

# 🔄 3. Cross-Site Request Forgery (CSRF)

## 📖 What is CSRF?

CSRF tricks authenticated users into performing unwanted actions without their knowledge.

---

## Example

A logged-in banking user visits a malicious website that secretly submits:

```text
Transfer ₹10,000 to attacker
```

The browser automatically includes the user's authentication cookie.

---

## Impact

- Unauthorized transactions
- Password changes
- Account modifications

---

## Prevention

- CSRF Tokens
- SameSite Cookies
- User Re-authentication
- Validate HTTP Referer

---

# 💻 4. Command Injection

## 📖 What is Command Injection?

An attacker executes operating system commands through vulnerable application inputs.

---

## Example

Vulnerable Application

```bash
ping 192.168.1.1
```

Attacker Input

```bash
127.0.0.1 && whoami
```

Executed Command

```bash
ping 127.0.0.1 && whoami
```

The attacker successfully executes an OS command.

---

## Prevention

- Never execute user input directly.
- Validate all inputs.
- Use allowlists.
- Avoid shell execution when possible.

---

# 📂 5. File Inclusion

## 📖 What is File Inclusion?

Attackers force applications to load unauthorized local or remote files.

Types:

- Local File Inclusion (LFI)
- Remote File Inclusion (RFI)

---

## Example

```text
https://example.com?page=admin.php
```

Attacker modifies it:

```text
?page=../../etc/passwd
```

---

## Impact

- Sensitive file disclosure
- Remote code execution
- Server compromise

---

## Prevention

- Validate file paths.
- Disable remote file inclusion.
- Use allowlists.

---

# 📁 6. Directory Traversal

## 📖 What is Directory Traversal?

Attackers access files outside the application's intended directory.

---

## Example

```text
../../../../etc/passwd
```

---

## Impact

- Read system files
- Expose configuration files
- Leak credentials

---

## Prevention

- Normalize file paths.
- Validate user input.
- Restrict file permissions.

---

# 🌍 7. Server-Side Request Forgery (SSRF)

## 📖 What is SSRF?

SSRF tricks a server into making requests to internal or external systems.

---

## Example

Application accepts:

```text
https://example.com/image.png
```

Attacker provides:

```text
http://169.254.169.254/latest/meta-data/
```

This may expose cloud instance metadata.

---

## Prevention

- Validate URLs.
- Use allowlists.
- Block private IP ranges.
- Disable unnecessary outbound requests.

---

# 📄 8. XML External Entity (XXE)

## 📖 What is XXE?

XXE occurs when XML parsers process external entities supplied by attackers.

---

## Example

```xml
<!DOCTYPE test [
<!ENTITY secret SYSTEM "file:///etc/passwd">
]>
```

---

## Impact

- Read sensitive files
- Server-side request forgery
- Denial of Service

---

## Prevention

- Disable external entities.
- Use secure XML parsers.
- Validate XML input.

---

# 🖱️ 9. Clickjacking

## 📖 What is Clickjacking?

Attackers trick users into clicking hidden buttons or links.

---

## Example

A fake webpage hides a banking transfer button beneath an attractive image.

---

## Prevention

- X-Frame-Options Header
- Content Security Policy
- Frame Busting Scripts

---

# 🔑 10. Brute Force Attack

## 📖 What is a Brute Force Attack?

Attackers repeatedly try different username and password combinations until they find the correct credentials.

---

## Example

```text
admin / admin
admin / password
admin / 123456
admin / qwerty
...
```

---

## Prevention

- Strong passwords
- Account lockout
- Multi-Factor Authentication (MFA)
- Rate limiting
- CAPTCHA

---

# 📊 Summary Table

| Attack | Target | Prevention |
|---------|--------|------------|
| SQL Injection | Database | Prepared Statements |
| XSS | Browser | Output Encoding |
| CSRF | User Session | CSRF Tokens |
| Command Injection | Operating System | Input Validation |
| File Inclusion | Server Files | File Validation |
| Directory Traversal | File System | Path Validation |
| SSRF | Internal Services | URL Validation |
| XXE | XML Parser | Disable External Entities |
| Clickjacking | User Interface | X-Frame-Options |
| Brute Force | Login System | MFA & Rate Limiting |

---

# 🛠️ DevSecOps Tools to Detect Web Attacks

| Tool | Purpose |
|------|----------|
| OWASP ZAP | Dynamic Security Testing (DAST) |
| Burp Suite | Web Application Security Testing |
| SonarQube | Static Code Analysis (SAST) |
| Trivy | Dependency & Container Scanning |
| GitLeaks | Secret Detection |
| ModSecurity | Web Application Firewall (WAF) |

---

# 💻 Example: Scan a Web Application Using OWASP ZAP

```bash
# Run a quick security scan against a web application
zap.sh -quickurl https://example.com
```

### Explanation

- Launches an automated DAST scan.
- Detects common vulnerabilities such as XSS, SQL Injection, and security misconfigurations.
- Generates a detailed security report for developers.

---

# 🌍 Real-World Scenario

An e-commerce website accepts user search input without validation.

An attacker enters a malicious SQL query into the search box.

↓

The application executes the query.

↓

Customer records are exposed.

↓

The organization suffers a data breach.

If input validation and prepared statements had been implemented, the attack would have failed.

---

# 🚀 Best Practices to Prevent Web Attacks

- Validate all user input.
- Use parameterized SQL queries.
- Escape HTML output.
- Enable HTTPS everywhere.
- Keep software dependencies updated.
- Apply security patches regularly.
- Enable Web Application Firewalls (WAF).
- Perform regular vulnerability scans.
- Integrate SAST and DAST into CI/CD pipelines.
- Monitor application logs continuously.

---

# 🎤 Interview Questions

### 1. What is SQL Injection?

SQL Injection is a vulnerability where attackers inject malicious SQL commands into database queries to manipulate or access data.

---

### 2. What is Cross-Site Scripting (XSS)?

XSS is an attack where malicious JavaScript is injected into web pages and executed in users' browsers.

---

### 3. What is the difference between XSS and CSRF?

| XSS | CSRF |
|-----|------|
| Executes malicious scripts in the victim's browser | Tricks authenticated users into performing unwanted actions |
| Targets website users | Exploits trusted user sessions |

---

### 4. What is SSRF?

Server-Side Request Forgery allows attackers to force a server to send requests to internal or external resources.

---

### 5. Which OWASP tool is commonly used to detect web vulnerabilities?

**OWASP ZAP** is a popular open-source Dynamic Application Security Testing (DAST) tool.

---

### 6. How can SQL Injection be prevented?

- Prepared Statements
- Parameterized Queries
- Input Validation
- Least Privilege Database Access

---

# 📝 Summary

Web applications are constantly exposed to cyber threats such as **SQL Injection, XSS, CSRF, Command Injection, SSRF, Directory Traversal, and Brute Force attacks**. Understanding these attacks and implementing secure coding practices, automated security testing, and continuous monitoring are essential components of a successful DevSecOps strategy. By integrating security throughout the Software Development Life Cycle (SDLC), organizations can significantly reduce the risk of exploitation and build resilient, secure web applications.

---

# 🤝 Contribute

Contributions are welcome! Feel free to fork this repository, improve the content, and submit a pull request.

---



---