# 🐳 Container Image Scanning

---

# 📖 Introduction

Containers have become the standard way to package and deploy applications in modern DevOps and cloud-native environments. A **container image** contains everything needed to run an application, including the operating system packages, runtime, libraries, dependencies, and application code.

If a container image contains vulnerable software, every container created from that image inherits those vulnerabilities. Therefore, **Container Image Scanning** is a critical DevSecOps practice that identifies security vulnerabilities, misconfigurations, exposed secrets, and compliance issues before an image is deployed.

Tools like **Trivy**, **Grype**, **Docker Scout**, **Clair**, and **Snyk** help automate container security throughout the software development lifecycle.

> **"A secure deployment starts with a secure container image."**

---

# 🎯 Objectives

After reading this guide, you will understand:

- What Container Image Scanning is
- Why it is important
- How image scanning works
- Components of a container image
- Common vulnerabilities
- Popular scanning tools
- CI/CD integration
- Best practices
- Interview questions

---

# 📖 What is Container Image Scanning?

**Container Image Scanning** is the process of analyzing a Docker or OCI container image to identify:

- Known vulnerabilities (CVEs)
- Outdated packages
- Operating system vulnerabilities
- Application dependency vulnerabilities
- Misconfigurations
- Exposed secrets
- License compliance issues

The scan is performed **before** the image is deployed to production.

---

# 🚀 Why is Container Image Scanning Important?

Without image scanning:

- Vulnerable images reach production.
- Attackers can exploit outdated packages.
- Secrets may be exposed inside images.
- Compliance requirements may not be met.
- Supply chain attacks become easier.

With image scanning:

- Security risks are detected early.
- Vulnerable packages are identified quickly.
- Deployments become safer.
- Compliance improves.
- CI/CD pipelines become more secure.

---

# 🏗️ Components of a Container Image

A typical container image contains multiple layers.

```text
Container Image

│
├── Application Code
├── Application Dependencies
├── Runtime (Java, Python, Node.js)
├── System Libraries
├── Operating System Packages
└── Base Image (Ubuntu, Alpine, Debian)
```

Every layer can introduce security vulnerabilities.

---

# 🔄 Container Image Scanning Workflow

```text
Developer
      │
      ▼
Docker Build
      │
      ▼
Container Image
      │
      ▼
Image Scanner
      │
      ▼
Identify Packages
      │
      ▼
Compare with CVE Database
      │
      ▼
Generate Security Report
      │
      ▼
Deploy Only If Secure
```

---

# ⚠️ Common Vulnerabilities Found

## 1️⃣ Operating System Vulnerabilities

Example:

```text
OpenSSL

Severity: Critical

CVE-2023-XXXX
```

---

## 2️⃣ Application Dependency Vulnerabilities

Example:

```text
Log4j

Version: 2.14.1

Critical Vulnerability Found
```

---

## 3️⃣ Exposed Secrets

Examples:

- AWS Access Keys
- API Tokens
- Database Passwords
- SSH Private Keys

---

## 4️⃣ Insecure Base Images

Example:

```dockerfile
FROM ubuntu:16.04
```

Old base images may contain hundreds of known vulnerabilities.

---

## 5️⃣ Misconfigurations

Examples:

- Running as root
- Weak file permissions
- Unnecessary packages
- Missing security updates

---

# 🛠️ Popular Container Image Scanning Tools

| Tool | Purpose |
|------|----------|
| Trivy | Vulnerability, Secret & Misconfiguration Scanning |
| Grype | Container Vulnerability Scanner |
| Docker Scout | Docker Image Security |
| Clair | Static Container Analysis |
| Snyk | Container & Dependency Scanning |
| Anchore Engine | Enterprise Image Scanning |
| Prisma Cloud | Cloud Native Security |

---

# 💻 Build a Docker Image

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html
```

Build the image:

```bash
docker build -t myapp:v1 .
```

### Explanation

- Creates a Docker image.
- Uses the official Nginx base image.
- Copies the application into the image.

---

# 💻 Scan an Image with Trivy

```bash
trivy image myapp:v1
```

### Explanation

- Downloads the latest vulnerability database.
- Scans every image layer.
- Checks OS packages and dependencies.
- Reports vulnerabilities by severity.

---

# 💻 Scan with Docker Scout

```bash
docker scout quickview myapp:v1
```

### Explanation

- Analyzes the container image.
- Displays vulnerabilities.
- Suggests more secure base images.
- Provides remediation recommendations.

---

# 💻 Scan with Grype

```bash
grype myapp:v1
```

### Explanation

- Identifies installed packages.
- Maps them against vulnerability databases.
- Generates a detailed security report.

---

# 📊 Sample Scan Report

```text
Target

myapp:v1

Critical : 1

High      : 4

Medium    : 7

Low       : 9
```

Example:

```text
Package

OpenSSL

Version

1.1.1

Severity

Critical

Fix Version

3.0.2
```

---

# ☁️ Container Image Scanning in DevSecOps

```text
Developer
      │
      ▼
Git Push
      │
      ▼
CI Pipeline
      │
      ├── Build
      ├── Unit Tests
      ├── SAST
      ├── Dependency Scan
      ├── Image Scan
      ▼
Push Image to Registry
      ▼
Deploy
```

Container images should always be scanned before they are pushed to a registry or deployed.

---

# 🌍 Real-World Scenario

A developer builds a Docker image for a banking application.

↓

The CI/CD pipeline automatically runs:

```bash
trivy image banking-app:v1
```

↓

The scanner reports:

```text
Critical Vulnerability

OpenSSL

Severity: Critical
```

↓

The pipeline fails.

↓

The developer updates the base image.

↓

The image is rebuilt.

↓

The scanner reports no Critical vulnerabilities.

↓

The secure image is pushed to the container registry.

---

# 🚀 Best Practices

- Scan every image before deployment.
- Use minimal base images such as Alpine or Distroless where appropriate.
- Keep base images updated regularly.
- Remove unnecessary packages.
- Avoid embedding secrets inside images.
- Use trusted image registries.
- Sign container images using Cosign or Sigstore.
- Automate image scanning in CI/CD pipelines.
- Continuously monitor images for newly discovered CVEs.
- Rebuild images whenever security patches are released.

---

# 📊 Container Image Scanning vs Dependency Scanning

| Container Image Scanning | Dependency Scanning |
|--------------------------|---------------------|
| Scans Docker/OCI images | Scans application dependencies |
| Detects OS package vulnerabilities | Detects library vulnerabilities |
| Includes image layers | Focuses on project packages |
| Can detect image misconfigurations | Does not analyze container layers |
| Includes operating system analysis | Focuses on application dependencies |

Using both provides comprehensive security coverage.

---

# 🎤 Interview Questions

### 1. What is Container Image Scanning?

Container Image Scanning is the process of analyzing container images for vulnerabilities, outdated packages, exposed secrets, and security misconfigurations before deployment.

---

### 2. Why is Container Image Scanning important?

It prevents vulnerable container images from reaching production, reducing the risk of security breaches and software supply chain attacks.

---

### 3. Name some Container Image Scanning tools.

- Trivy
- Grype
- Docker Scout
- Clair
- Snyk
- Anchore Engine

---

### 4. What does `trivy image` do?

It scans a Docker or OCI container image for known vulnerabilities, secrets, and misconfigurations, then generates a detailed security report.

---

### 5. Why should you keep base images updated?

Outdated base images may contain known security vulnerabilities that can be inherited by every application built on top of them.

---

### 6. How is Container Image Scanning integrated into DevSecOps?

Container Image Scanning is automated within CI/CD pipelines after the image is built. Images that fail security policies are blocked from being pushed to registries or deployed to production.

---

# 📝 Summary

Container Image Scanning is a fundamental DevSecOps practice that helps secure Docker and OCI images by detecting vulnerabilities, outdated packages, secrets, and configuration issues before deployment. By integrating tools like **Trivy**, **Docker Scout**, and **Grype** into CI/CD pipelines, organizations can ensure only secure container images are published and deployed, significantly reducing software supply chain risks.

---

# 🤝 Contribute

Contributions are welcome! Feel free to fork this repository, improve the content, and submit a pull request.

---

# 👨‍💻 Author



---