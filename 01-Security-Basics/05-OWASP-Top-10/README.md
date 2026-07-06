# 🛡️ OWASP Top 10

---

# 📖 Introduction

The **OWASP Top 10** is one of the most recognized cybersecurity awareness documents for web application security. It lists the **10 most critical security risks** affecting modern web applications based on data collected from security experts and organizations worldwide.

It is published by the **Open Worldwide Application Security Project (OWASP)**, a non-profit organization dedicated to improving software security.

The OWASP Top 10 serves as a guideline for developers, DevOps engineers, security professionals, and organizations to identify, prevent, and mitigate common web application vulnerabilities.

> **"Build secure applications by understanding the most common security risks first."**

---

# 🎯 Objectives of OWASP Top 10

The primary objectives are:

- Identify the most critical web application vulnerabilities.
- Help developers write secure code.
- Raise security awareness.
- Reduce application security risks.
- Improve secure software development practices.
- Integrate security into the DevSecOps lifecycle.

---

# 🌐 What is OWASP?

**OWASP (Open Worldwide Application Security Project)** is a global non-profit organization that provides free tools, documentation, methodologies, and educational resources for application security.

### Popular OWASP Projects

- OWASP Top 10
- OWASP ZAP
- OWASP ASVS
- OWASP Dependency-Check
- OWASP Cheat Sheet Series
- OWASP WebGoat

---

# 🏗️ OWASP Top 10 (2021)

| No. | Vulnerability | Risk ID |
|-----|---------------|----------|
| 1 | Broken Access Control | A01:2021 |
| 2 | Cryptographic Failures | A02:2021 |
| 3 | Injection | A03:2021 |
| 4 | Insecure Design | A04:2021 |
| 5 | Security Misconfiguration | A05:2021 |
| 6 | Vulnerable and Outdated Components | A06:2021 |
| 7 | Identification and Authentication Failures | A07:2021 |
| 8 | Software and Data Integrity Failures | A08:2021 |
| 9 | Security Logging and Monitoring Failures | A09:2021 |
| 10 | Server-Side Request Forgery (SSRF) | A10:2021 |

---

# 🔍 1. Broken Access Control (A01:2021)

## 📖 Description

Broken Access Control occurs when users can access resources or perform actions beyond their authorized permissions.

### Example

A normal user changes the URL:

```text
/admin/dashboard
```

Instead of:

```text
/user/dashboard
```

If the application allows access without proper authorization checks, the user gains administrative privileges.

### Prevention

- Implement Role-Based Access Control (RBAC).
- Apply the Principle of Least Privilege (PoLP).
- Validate authorization on the server side.

---

# 🔐 2. Cryptographic Failures (A02:2021)

## 📖 Description

Sensitive data is exposed because of weak encryption, improper key management, or transmitting data without encryption.

### Example

Using HTTP instead of HTTPS.

### Prevention

- Use HTTPS (TLS).
- Encrypt sensitive data.
- Store passwords using strong hashing algorithms such as **bcrypt** or **Argon2**.
- Rotate encryption keys regularly.

---

# 💉 3. Injection (A03:2021)

## 📖 Description

Injection vulnerabilities occur when untrusted user input is interpreted as commands or queries.

Common injection attacks include:

- SQL Injection
- NoSQL Injection
- OS Command Injection
- LDAP Injection

### Example

```sql
SELECT * FROM users
WHERE username = 'admin'
AND password = '12345';
```

If user input is not validated, attackers may manipulate the query.

### Prevention

- Use Prepared Statements.
- Validate user input.
- Use parameterized queries.
- Apply input sanitization.

---

# 🏗️ 4. Insecure Design (A04:2021)

## 📖 Description

Applications designed without security considerations become vulnerable regardless of secure coding practices.

### Example

An application allows unlimited login attempts without rate limiting.

### Prevention

- Perform threat modeling.
- Design with security in mind.
- Conduct architecture reviews.
- Apply secure design principles.

---

# ⚙️ 5. Security Misconfiguration (A05:2021)

## 📖 Description

Improperly configured servers, applications, cloud services, or containers expose systems to attackers.

### Examples

- Default passwords
- Open S3 buckets
- Unused services enabled
- Debug mode enabled in production

### Prevention

- Disable unnecessary services.
- Remove default credentials.
- Regularly review configurations.
- Harden operating systems and servers.

---

# 📦 6. Vulnerable and Outdated Components (A06:2021)

## 📖 Description

Applications use libraries, frameworks, or software with known vulnerabilities.

### Example

Using an outdated version of Log4j vulnerable to Log4Shell.

### Prevention

- Regularly update dependencies.
- Perform dependency scanning.
- Remove unused libraries.
- Maintain an inventory of software components.

---

# 🔑 7. Identification and Authentication Failures (A07:2021)

## 📖 Description

Weak authentication mechanisms allow attackers to impersonate users.

### Examples

- Weak passwords
- No Multi-Factor Authentication (MFA)
- Predictable session IDs

### Prevention

- Enforce strong password policies.
- Enable MFA.
- Secure session management.
- Lock accounts after repeated failed login attempts.

---

# 🔄 8. Software and Data Integrity Failures (A08:2021)

## 📖 Description

Applications fail to verify the integrity of software updates, CI/CD pipelines, or critical data.

### Example

Installing packages from untrusted repositories without verification.

### Prevention

- Verify software signatures.
- Use trusted repositories.
- Protect CI/CD pipelines.
- Validate update integrity.

---

# 📊 9. Security Logging and Monitoring Failures (A09:2021)

## 📖 Description

Organizations fail to detect attacks because of insufficient logging and monitoring.

### Example

Failed login attempts are never logged or reviewed.

### Prevention

- Enable centralized logging.
- Monitor suspicious activities.
- Configure security alerts.
- Retain logs securely.

---

# 🌍 10. Server-Side Request Forgery (SSRF) (A10:2021)

## 📖 Description

SSRF allows attackers to trick a server into making requests to unintended internal or external systems.

### Example

An application fetches URLs provided by users without validation.

### Prevention

- Validate URLs.
- Use allowlists.
- Block internal IP ranges.
- Disable unnecessary outbound network access.

---

# 📊 Summary Table

| Risk ID | Vulnerability | Example |
|-----------|---------------|---------|
| A01 | Broken Access Control | Unauthorized admin access |
| A02 | Cryptographic Failures | Unencrypted sensitive data |
| A03 | Injection | SQL Injection |
| A04 | Insecure Design | Missing rate limiting |
| A05 | Security Misconfiguration | Default credentials |
| A06 | Vulnerable Components | Outdated libraries |
| A07 | Authentication Failures | Weak passwords |
| A08 | Integrity Failures | Unverified software updates |
| A09 | Logging Failures | Missing security logs |
| A10 | SSRF | Accessing internal services |

---

# 🛠️ DevSecOps Tools for OWASP Risks

| Security Area | Popular Tools |
|---------------|---------------|
| Static Code Analysis | SonarQube |
| Dynamic Testing | OWASP ZAP |
| Dependency Scanning | Trivy, OWASP Dependency-Check |
| Secret Detection | GitLeaks |
| Container Security | Trivy |
| Infrastructure Security | Checkov |

---

# 💻 Example: Scan a Web Application with OWASP ZAP

```bash
# Start an automated OWASP ZAP scan
zap.sh -quickurl https://example.com
```

### Explanation

- Launches a quick security scan against the target web application.
- Identifies common vulnerabilities such as SQL Injection, XSS, and security misconfigurations.
- Generates a report for developers to fix identified issues before deployment.

---

# 🌍 Real-World Scenario

A developer deploys a web application with:

- Weak passwords
- Outdated dependencies
- Missing access control
- No HTTPS

An attacker exploits these weaknesses and gains unauthorized access to customer data.

If the development team had followed the **OWASP Top 10** recommendations, these vulnerabilities could have been detected and mitigated during development and testing.

---

# 🚀 Benefits of Following the OWASP Top 10

- Reduces common web application vulnerabilities.
- Improves application security.
- Enhances customer trust.
- Supports compliance requirements.
- Encourages secure coding practices.
- Strengthens DevSecOps pipelines.

---

# 💡 Best Practices

- Follow secure coding standards.
- Validate and sanitize all user input.
- Use HTTPS for all communications.
- Implement proper authentication and authorization.
- Perform regular vulnerability scans.
- Keep software dependencies updated.
- Conduct code reviews.
- Enable continuous monitoring and logging.
- Integrate security testing into CI/CD pipelines.

---

# 🎤 Interview Questions

### 1. What is the OWASP Top 10?

The OWASP Top 10 is a list of the ten most critical web application security risks published by OWASP.

---

### 2. What does OWASP stand for?

**Open Worldwide Application Security Project.**

---

### 3. What is the most critical risk in the OWASP Top 10 (2021)?

**Broken Access Control (A01:2021).**

---

### 4. Name three vulnerabilities from the OWASP Top 10.

- Injection
- Security Misconfiguration
- Cryptographic Failures

---

### 5. Which DevSecOps tool is commonly used for Dynamic Application Security Testing (DAST)?

**OWASP ZAP.**

---

### 6. Why should DevOps engineers understand the OWASP Top 10?

Because it helps them integrate security into CI/CD pipelines, identify common application vulnerabilities, and deploy secure applications.

---

# 📝 Summary

The **OWASP Top 10** is a globally recognized standard for identifying and mitigating the most critical web application security risks. Understanding these vulnerabilities enables developers, DevOps engineers, and security professionals to build secure applications, integrate automated security testing into DevSecOps pipelines, and reduce the risk of cyberattacks. Mastering the OWASP Top 10 is essential for anyone pursuing a career in cybersecurity or DevSecOps.

---

# 🤝 Contribute

Contributions are welcome! Feel free to fork this repository, improve the content, and submit a pull request.

---

# 👨‍💻 Author

**Aditya Jadhav**  
Beginner Cloud & DevOps Learner

📧 **adijadhav8446@gmail.com**  
🌐 **GitHub Profile:** https://github.com/AdiJadhav1608  
🔗 **LinkedIn:** https://www.linkedin.com/in/aditya-jadhav-718087339/

---