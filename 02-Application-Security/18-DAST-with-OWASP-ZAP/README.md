# 🌐 DAST with OWASP ZAP

---

# 📖 Introduction

Even if an application passes code reviews and Static Application Security Testing (SAST), it may still contain vulnerabilities that only appear **while the application is running**. To detect these runtime security issues, organizations use **Dynamic Application Security Testing (DAST)**.

**OWASP ZAP (Zed Attack Proxy)** is one of the world's most popular **open-source DAST tools**. It scans running web applications by simulating attacks just like a real attacker, helping identify vulnerabilities before software is deployed to production.

In DevSecOps, OWASP ZAP is integrated into CI/CD pipelines to automatically perform security testing on deployed applications.

> **"Test your application the way an attacker would."**

---

# 🎯 Objectives

After reading this guide, you will understand:

- What DAST is
- What OWASP ZAP is
- How OWASP ZAP works
- OWASP ZAP architecture
- Installing OWASP ZAP
- Running DAST scans
- CI/CD integration
- Best practices
- Interview questions

---

# 📖 What is DAST?

**Dynamic Application Security Testing (DAST)** is a security testing technique that analyzes a **running application** by interacting with it from the outside, just like a real user or attacker.

Unlike SAST, DAST does **not** require access to the application's source code.

---

# 🔍 What is OWASP ZAP?

**OWASP ZAP (Zed Attack Proxy)** is a free and open-source web application security scanner developed by the **OWASP Foundation**.

It works as an **intercepting proxy**, allowing security professionals and developers to inspect traffic between a browser and a web application while performing automated vulnerability scans.

---

# 🚀 Why Use OWASP ZAP?

OWASP ZAP helps detect:

- SQL Injection
- Cross-Site Scripting (XSS)
- Broken Authentication
- Security Misconfigurations
- Cross-Site Request Forgery (CSRF)
- Directory Traversal
- Sensitive Information Disclosure
- Missing Security Headers
- Weak SSL/TLS Configurations

---

# 🏗️ OWASP ZAP Architecture

```text
          Browser
             │
             ▼
      OWASP ZAP Proxy
             │
             ▼
      Target Web Application
             │
             ▼
    Vulnerability Detection
             │
             ▼
      Security Report
```

---

# 🔄 DAST Workflow

```text
Deploy Application
        │
        ▼
Start OWASP ZAP
        │
        ▼
Spider Website
        │
        ▼
Passive Scan
        │
        ▼
Active Scan
        │
        ▼
Generate Security Report
```

---

# 🔎 Types of Scans in OWASP ZAP

## 1️⃣ Spider Scan

Discovers all pages, links, forms, and endpoints within the web application.

---

## 2️⃣ Passive Scan

Analyzes HTTP requests and responses without sending malicious payloads.

Examples:

- Missing Security Headers
- Cookie Issues
- Information Disclosure

---

## 3️⃣ Active Scan

Sends attack payloads to identify vulnerabilities.

Examples:

- SQL Injection
- XSS
- Command Injection
- Path Traversal

---

## 4️⃣ AJAX Spider

Uses a browser engine to crawl JavaScript-heavy applications such as React, Angular, and Vue.js.

---

# ⚠️ Common Vulnerabilities Detected

| Vulnerability | Description |
|---------------|-------------|
| SQL Injection | Malicious SQL queries |
| Cross-Site Scripting (XSS) | Script injection into web pages |
| CSRF | Unauthorized requests on behalf of users |
| Directory Traversal | Access to restricted files |
| Security Headers Missing | Missing HTTP security headers |
| Session Issues | Weak session management |
| Cookie Misconfiguration | Insecure cookie settings |
| Information Disclosure | Exposure of sensitive information |

---

# 🛠️ Install OWASP ZAP

Ubuntu:

```bash
# Download OWASP ZAP
wget https://github.com/zaproxy/zaproxy/releases/latest/download/ZAP_2_16_0_unix.sh

# Make installer executable
chmod +x ZAP_2_16_0_unix.sh

# Run installer
./ZAP_2_16_0_unix.sh
```

### Explanation

- Downloads the installer.
- Grants execute permission.
- Installs OWASP ZAP.

---

# 🐳 Run OWASP ZAP Using Docker

```bash
# Pull the latest ZAP image
docker pull ghcr.io/zaproxy/zaproxy:stable

# Verify installation
docker images
```

### Explanation

- Downloads the official OWASP ZAP Docker image.
- Allows running scans without installing ZAP directly on the host.

---

# 💻 Quick Scan

```bash
# Perform a quick scan
zap.sh -quickurl http://example.com
```

### Explanation

- Starts OWASP ZAP.
- Scans the specified website.
- Generates a vulnerability report.

---

# 💻 Full Scan Using Docker

```bash
docker run -t ghcr.io/zaproxy/zaproxy:stable zap-full-scan.py \
-t http://example.com \
-r zap-report.html
```

### Explanation

- Launches the ZAP container.
- Performs a full security scan.
- Generates an HTML report named **zap-report.html**.

---

# 📊 Sample Scan Report

```text
High Risk      : 2

Medium Risk    : 5

Low Risk       : 8

Informational  : 14
```

Example findings:

```text
High

SQL Injection

Cross-Site Scripting (XSS)
```

---

# ☁️ OWASP ZAP in Jenkins Pipeline

```groovy
pipeline {
    agent any

    stages {

        stage('Deploy Test App') {
            steps {
                sh 'docker-compose up -d'
            }
        }

        stage('DAST Scan') {
            steps {
                sh '''
                docker run --rm \
                --network host \
                ghcr.io/zaproxy/zaproxy:stable \
                zap-baseline.py \
                -t http://localhost:8080
                '''
            }
        }
    }
}
```

### Explanation

- Deploys the application.
- Runs OWASP ZAP Baseline Scan.
- Reports security findings before production deployment.

---

# ☁️ DAST in DevSecOps Pipeline

```text
Developer
      │
      ▼
Git Push
      │
      ▼
CI/CD Pipeline
      │
      ├── Build
      ├── Unit Tests
      ├── SAST
      ├── Deploy to Test
      ├── DAST (OWASP ZAP)
      ▼
Production
```

DAST validates the application's security after deployment to a testing environment.

---

# 🌍 Real-World Scenario

A company deploys a new e-commerce application to a staging environment.

↓

The Jenkins pipeline automatically launches OWASP ZAP.

↓

OWASP ZAP performs:

- Spider Scan
- Passive Scan
- Active Scan

↓

The scan detects:

```text
Cross-Site Scripting (XSS)

Severity: High
```

↓

The deployment is stopped.

↓

Developers sanitize user input and encode output.

↓

A new scan passes successfully.

↓

The application is deployed to production.

---

# 🚀 Best Practices

- Run DAST on every release candidate.
- Scan staging environments before production deployment.
- Combine DAST with SAST and Dependency Scanning.
- Review High and Critical findings immediately.
- Secure authentication credentials used during scans.
- Keep OWASP ZAP updated.
- Automate scans in CI/CD pipelines.
- Validate and remediate findings before release.

---

# 📊 SAST vs DAST

| SAST | DAST |
|------|------|
| Analyzes source code | Tests running application |
| No application execution | Requires deployed application |
| Finds coding issues | Finds runtime vulnerabilities |
| Early SDLC | Testing phase |
| Faster scans | More realistic attack simulation |

Both approaches complement each other and should be used together.

---

# 🎤 Interview Questions

### 1. What is DAST?

Dynamic Application Security Testing (DAST) analyzes a running application by simulating attacks to identify runtime security vulnerabilities.

---

### 2. What is OWASP ZAP?

OWASP ZAP (Zed Attack Proxy) is an open-source Dynamic Application Security Testing (DAST) tool used to discover vulnerabilities in running web applications.

---

### 3. What is the difference between Passive Scan and Active Scan?

- **Passive Scan** analyzes HTTP traffic without attacking the application.
- **Active Scan** sends attack payloads to identify exploitable vulnerabilities.

---

### 4. What vulnerabilities can OWASP ZAP detect?

OWASP ZAP can detect SQL Injection, XSS, CSRF, Directory Traversal, missing security headers, session management issues, and other web application vulnerabilities.

---

### 5. Does OWASP ZAP require source code?

No. OWASP ZAP tests the application from the outside and does not require access to source code.

---

### 6. How is OWASP ZAP used in DevSecOps?

OWASP ZAP is integrated into CI/CD pipelines to automatically perform DAST scans on deployed applications before they are promoted to production.

---

# 📝 Summary

**OWASP ZAP** is one of the most widely used **Dynamic Application Security Testing (DAST)** tools for securing web applications. By simulating real-world attacks against running applications, it identifies vulnerabilities such as SQL Injection, Cross-Site Scripting (XSS), and security misconfigurations. Integrated into DevSecOps pipelines, OWASP ZAP helps teams detect runtime security issues early, automate security testing, and ensure that only secure applications are deployed to production.

---

# 🤝 Contribute

Contributions are welcome! Feel free to fork this repository, improve the content, and submit a pull request.

---

# 👨‍💻 Author


---