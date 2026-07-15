# 🔍 SAST vs DAST vs IAST

---

# 📖 Introduction

Modern applications face security threats throughout the Software Development Life Cycle (SDLC). To identify vulnerabilities early and improve software security, organizations use different types of application security testing.

The three most common security testing approaches are:

- **SAST (Static Application Security Testing)**
- **DAST (Dynamic Application Security Testing)**
- **IAST (Interactive Application Security Testing)**

Each technique identifies different types of vulnerabilities and is used at different stages of the DevSecOps pipeline. Understanding the differences helps organizations build a comprehensive application security strategy.

> **No single security testing method can find every vulnerability. Combining SAST, DAST, and IAST provides stronger application security.**

---

# 🎯 Objectives

After reading this guide, you will understand:

- What SAST is
- What DAST is
- What IAST is
- How each works
- Advantages and disadvantages
- Popular tools
- DevSecOps integration
- Interview questions

---

# 🏗️ Application Security Testing Overview

```text
Developer Writes Code
          │
          ▼
        SAST
(Source Code Analysis)
          │
          ▼
Build Application
          │
          ▼
Deploy to Test Environment
          │
          ▼
        DAST
(Running Application Scan)
          │
          ▼
Run Application with IAST Agent
          │
          ▼
        IAST
(Runtime Analysis)
          │
          ▼
Production Deployment
```

---

# 🔐 What is SAST?

## 📖 Definition

**SAST (Static Application Security Testing)** analyzes the application's **source code, bytecode, or binaries** without executing the application.

It detects vulnerabilities during development before the application is deployed.

---

## How SAST Works

```text
Source Code
      │
      ▼
SAST Scanner
      │
      ▼
Analyze Code
      │
      ▼
Security Report
```

---

## Common Vulnerabilities Detected

- SQL Injection
- Cross-Site Scripting (XSS)
- Hardcoded Passwords
- Weak Cryptography
- Buffer Overflow
- Code Quality Issues
- Security Misconfigurations

---

## Advantages

- Detects issues early
- Supports Shift Left Security
- Fast feedback for developers
- No running application required
- Easy CI/CD integration

---

## Limitations

- Cannot detect runtime issues
- May generate false positives
- Requires source code access

---

## Popular SAST Tools

- SonarQube
- Checkmarx
- Fortify
- Semgrep
- Veracode

---

# 🌐 What is DAST?

## 📖 Definition

**DAST (Dynamic Application Security Testing)** analyzes a **running application** by simulating attacks from the outside, similar to how a real attacker interacts with the application.

---

## How DAST Works

```text
Running Application
        │
        ▼
DAST Scanner
        │
        ▼
Attack Simulation
        │
        ▼
Security Report
```

---

## Common Vulnerabilities Detected

- SQL Injection
- XSS
- Authentication Issues
- Security Misconfiguration
- Broken Access Control
- SSRF
- CSRF

---

## Advantages

- No source code required
- Simulates real-world attacks
- Detects runtime vulnerabilities
- Technology independent

---

## Limitations

- Requires deployed application
- Cannot identify the exact vulnerable code line
- Slower than SAST

---

## Popular DAST Tools

- OWASP ZAP
- Burp Suite
- Acunetix
- Invicti
- AppSpider

---

# ⚡ What is IAST?

## 📖 Definition

**IAST (Interactive Application Security Testing)** combines the strengths of SAST and DAST by monitoring the application **while it is running** using an instrumentation agent.

It analyzes both application behavior and source code during testing.

---

## How IAST Works

```text
Running Application
        │
        ▼
IAST Agent
        │
        ▼
Monitor Runtime
        │
        ▼
Detect Vulnerabilities
        │
        ▼
Security Report
```

---

## Common Vulnerabilities Detected

- SQL Injection
- XSS
- Command Injection
- Authentication Flaws
- Configuration Issues
- Insecure APIs

---

## Advantages

- More accurate results
- Lower false positives
- Identifies exact vulnerable code
- Runtime visibility

---

## Limitations

- Requires an IAST agent
- Slight runtime overhead
- More complex setup

---

## Popular IAST Tools

- Contrast Security
- Seeker
- Hdiv
- Synopsys Seeker

---

# 📊 SAST vs DAST vs IAST

| Feature | SAST | DAST | IAST |
|---------|------|------|------|
| Full Form | Static Application Security Testing | Dynamic Application Security Testing | Interactive Application Security Testing |
| Source Code Required | ✅ Yes | ❌ No | ✅ Usually Yes |
| Running Application Required | ❌ No | ✅ Yes | ✅ Yes |
| Testing Stage | Development | Testing | Testing |
| Finds Runtime Issues | ❌ No | ✅ Yes | ✅ Yes |
| Detects Code-Level Issues | ✅ Yes | ❌ No | ✅ Yes |
| False Positives | Higher | Medium | Lower |
| Speed | Fast | Medium | Medium |
| Best For | Early Detection | Runtime Security | Accurate Runtime Analysis |

---

# 🔄 When to Use Each?

| Stage | Security Testing |
|--------|------------------|
| Code Development | SAST |
| Test Environment | DAST |
| Runtime Testing | IAST |
| Production Monitoring | RASP / SIEM / Monitoring |

---

# 🛠️ DevSecOps Pipeline Integration

```text
Developer
     │
     ▼
Git Push
     │
     ▼
CI Pipeline
     │
     ├── SAST Scan
     ├── Secret Scan
     ├── Dependency Scan
     ▼
Build
     │
     ▼
Deploy to Test
     │
     ├── DAST Scan
     ├── IAST Analysis
     ▼
Deploy to Production
     │
     ▼
Monitoring & Logging
```

---

# 💻 Example 1: SAST with SonarQube

```bash
# Run SonarQube analysis
sonar-scanner
```

### Explanation

- Analyzes source code.
- Detects bugs and security vulnerabilities.
- Generates a detailed security report before deployment.

---

# 💻 Example 2: DAST with OWASP ZAP

```bash
# Perform a quick scan on a running application
zap.sh -quickurl https://example.com
```

### Explanation

- Scans a live application.
- Simulates attacks.
- Detects runtime vulnerabilities.

---

# 🌍 Real-World Scenario

A company develops an online banking application.

### During Development

Developers use **SAST** to detect SQL Injection and hardcoded credentials.

↓

### During Testing

Security engineers run **DAST** to identify authentication flaws and XSS vulnerabilities.

↓

### During QA

The application is instrumented with an **IAST** agent, which identifies the exact vulnerable source code responsible for a runtime issue.

↓

### Production

The application is deployed with significantly fewer security vulnerabilities.

---

# 🚀 Best Practices

- Use SAST during development.
- Perform DAST before every release.
- Use IAST in QA environments.
- Automate security testing in CI/CD.
- Combine all three approaches for maximum coverage.
- Fix critical vulnerabilities immediately.
- Review security reports regularly.
- Keep security tools updated.

---

# 📊 Quick Comparison

| Category | SAST | DAST | IAST |
|----------|------|------|------|
| White Box Testing | ✅ | ❌ | ✅ |
| Black Box Testing | ❌ | ✅ | ❌ |
| Runtime Visibility | ❌ | Limited | ✅ |
| Code Visibility | ✅ | ❌ | ✅ |
| CI/CD Friendly | ✅ | ✅ | ✅ |

---

# 🎤 Interview Questions

### 1. What is SAST?

SAST (Static Application Security Testing) analyzes source code without executing the application to identify security vulnerabilities early in development.

---

### 2. What is DAST?

DAST (Dynamic Application Security Testing) tests a running application by simulating external attacks to identify runtime vulnerabilities.

---

### 3. What is IAST?

IAST (Interactive Application Security Testing) combines runtime analysis with code-level visibility using an instrumentation agent to provide accurate vulnerability detection.

---

### 4. What is the difference between SAST and DAST?

- **SAST** analyzes source code without executing the application.
- **DAST** analyzes a running application from the outside.

---

### 5. Which testing method requires a running application?

**DAST** and **IAST** require the application to be running.

---

### 6. Which testing approach is best?

There is no single best approach. A strong DevSecOps pipeline combines **SAST**, **DAST**, and **IAST** to achieve comprehensive application security.

---

# 📝 Summary

**SAST**, **DAST**, and **IAST** are complementary application security testing techniques used throughout the DevSecOps lifecycle. SAST identifies vulnerabilities early by analyzing source code, DAST evaluates running applications from an attacker's perspective, and IAST provides deep runtime analysis with code-level insights. Together, they enable organizations to detect vulnerabilities earlier, improve software quality, and build secure applications before deployment.

---

# 🤝 Contribute

Contributions are welcome! Feel free to fork this repository, improve the content, and submit a pull request.

---

# 👨‍💻 Author



---