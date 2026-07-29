# 🛡️ Trivy Introduction

---

# 📖 Introduction

Modern applications consist of **source code, third-party libraries, container images, Kubernetes manifests, and Infrastructure as Code (IaC)**. Every one of these components can contain security vulnerabilities or misconfigurations.

**Trivy** is a fast, open-source security scanner developed by **Aqua Security**. It helps developers and DevSecOps engineers detect **vulnerabilities, misconfigurations, exposed secrets, and license issues** in applications before they reach production.

Trivy is widely used in DevSecOps pipelines because it is lightweight, easy to use, and supports scanning multiple targets with a single tool.

> **"Scan everything before you deploy anything."**

---

# 🎯 Objectives

After reading this guide, you will understand:

- What Trivy is
- Why Trivy is important
- Features of Trivy
- What Trivy can scan
- How Trivy works
- Installing Trivy
- Basic scanning commands
- DevSecOps integration
- Best practices
- Interview questions

---

# 📖 What is Trivy?

**Trivy** is an open-source security scanner that detects:

- Vulnerabilities (CVEs)
- Misconfigurations
- Exposed Secrets
- License Issues

It supports scanning:

- Container Images
- Filesystems
- Git Repositories
- Kubernetes Clusters
- Infrastructure as Code (Terraform, CloudFormation, Kubernetes YAML)
- SBOMs (Software Bill of Materials)

---

# 🚀 Why Use Trivy?

Without Trivy:

- Vulnerable container images may be deployed.
- Outdated packages may remain unnoticed.
- Secrets may be accidentally exposed.
- Infrastructure misconfigurations may go undetected.
- Compliance becomes more difficult.

With Trivy:

- Security vulnerabilities are detected early.
- Misconfigurations are identified automatically.
- Secrets are discovered before deployment.
- CI/CD security is improved.
- Software Supply Chain Security is strengthened.

---

# 🔍 What Can Trivy Scan?

| Scan Target | Description |
|-------------|-------------|
| Container Images | Scan Docker and OCI images |
| Filesystem | Scan local project files |
| Git Repository | Scan application source code |
| Kubernetes | Scan cluster resources |
| IaC | Scan Terraform, Kubernetes YAML, CloudFormation |
| SBOM | Scan Software Bill of Materials |
| Root Filesystem | Scan operating system packages |

---

# 🏗️ Trivy Architecture

```text
Developer
     │
     ▼
Application / Container / IaC
     │
     ▼
        Trivy
     │
     ▼
Download Vulnerability Database
     │
     ▼
Analyze Components
     │
     ▼
Generate Security Report
```

---

# 🔄 How Trivy Works

```text
Select Scan Target
        │
        ▼
Download Vulnerability Database
        │
        ▼
Identify Installed Packages
        │
        ▼
Compare with CVE Database
        │
        ▼
Generate Report
```

---

# 🔐 Types of Security Checks

## 1️⃣ Vulnerability Scanning

Detects known software vulnerabilities using CVE databases.

Example:

```text
Package:

openssl

Version:

1.1.1k

Result:

High Severity Vulnerability Found
```

---

## 2️⃣ Misconfiguration Scanning

Detects insecure Infrastructure as Code (IaC) configurations.

Example:

```yaml
resource "aws_s3_bucket" "demo" {
  bucket = "my-bucket"
}
```

Trivy may report that encryption or public access restrictions are missing.

---

## 3️⃣ Secret Scanning

Detects:

- AWS Keys
- API Keys
- Passwords
- Tokens
- SSH Private Keys

Example:

```python
AWS_SECRET_KEY = "my-secret-key"
```

---

## 4️⃣ License Scanning

Identifies software licenses used by project dependencies.

Examples:

- MIT
- Apache 2.0
- GPL
- BSD

---

# 🛠️ Install Trivy

Ubuntu:

```bash
# Install Trivy
sudo apt-get install wget apt-transport-https gnupg lsb-release

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/trivy.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] \
https://aquasecurity.github.io/trivy-repo/deb \
$(lsb_release -sc) main" | \
sudo tee /etc/apt/sources.list.d/trivy.list

sudo apt update

sudo apt install trivy
```

### Verify Installation

```bash
trivy --version
```

---

# 💻 Scan a Filesystem

```bash
trivy fs .
```

### Explanation

- Scans the current project directory.
- Detects vulnerable dependencies.
- Checks for secrets and misconfigurations.
- Generates a security report.

---

# 💻 Scan a Docker Image

```bash
trivy image nginx:latest
```

### Explanation

- Downloads the latest vulnerability database.
- Scans all packages inside the Docker image.
- Displays vulnerabilities with severity levels.

---

# 💻 Scan a Git Repository

```bash
trivy repo https://github.com/example/project
```

### Explanation

- Downloads the repository.
- Scans dependencies.
- Detects secrets and vulnerabilities.
- Reports findings.

---

# 💻 Scan Infrastructure as Code

```bash
trivy config .
```

### Explanation

- Scans Terraform files.
- Scans Kubernetes YAML manifests.
- Scans CloudFormation templates.
- Detects security misconfigurations.

---

# 📊 Sample Output

```text
Target: nginx:latest

Total Vulnerabilities

CRITICAL : 1

HIGH     : 3

MEDIUM   : 5

LOW      : 4
```

---

# ☁️ Trivy in DevSecOps Pipeline

```text
Developer
      │
      ▼
Git Push
      │
      ▼
CI/CD Pipeline
      │
      ├── SAST
      ├── Dependency Scan
      ├── Secret Scan
      ├── Trivy Image Scan
      ├── IaC Scan
      ▼
Deploy
```

Trivy is commonly executed before deployment to ensure applications and infrastructure meet security requirements.

---

# 🌍 Real-World Scenario

A developer builds a Docker image for a web application.

↓

The Jenkins pipeline automatically runs:

```bash
trivy image myapp:latest
```

↓

Trivy detects:

```text
Critical Vulnerability

openssl

Severity: CRITICAL
```

↓

The pipeline fails.

↓

The developer updates the vulnerable package.

↓

The image is rebuilt.

↓

A new Trivy scan reports no Critical vulnerabilities.

↓

The image is deployed to production.

---

# 🚀 Best Practices

- Scan every Docker image before deployment.
- Scan Infrastructure as Code files.
- Perform filesystem scans during development.
- Keep the Trivy vulnerability database updated.
- Fail CI/CD pipelines on Critical vulnerabilities.
- Scan for exposed secrets regularly.
- Combine Trivy with SAST and DAST tools.
- Generate and scan SBOMs for releases.
- Review vulnerability reports after every scan.

---

# 📊 Trivy vs OWASP Dependency-Check

| Trivy | OWASP Dependency-Check |
|--------|------------------------|
| Scans container images | Scans project dependencies |
| Supports IaC scanning | Focuses on dependencies |
| Secret scanning | No built-in secret scanning |
| Kubernetes support | Limited |
| SBOM support | Limited |
| Fast and lightweight | More dependency-focused |

Both tools complement each other and can be used together.

---

# 🎤 Interview Questions

### 1. What is Trivy?

Trivy is an open-source security scanner that detects vulnerabilities, secrets, misconfigurations, and license issues in containers, applications, Infrastructure as Code, and Kubernetes resources.

---

### 2. What can Trivy scan?

Trivy can scan:

- Container Images
- Filesystems
- Git Repositories
- Kubernetes Clusters
- Infrastructure as Code
- SBOMs
- Operating System Packages

---

### 3. What is the purpose of `trivy image`?

It scans a Docker or OCI container image for known vulnerabilities in operating system packages and installed application dependencies.

---

### 4. What does `trivy config` do?

It scans Infrastructure as Code files such as Terraform, Kubernetes YAML, and CloudFormation templates for security misconfigurations.

---

### 5. Can Trivy detect secrets?

Yes. Trivy can detect exposed API keys, passwords, tokens, SSH keys, and other sensitive credentials.

---

### 6. How is Trivy used in DevSecOps?

Trivy is integrated into CI/CD pipelines to automatically scan source code, dependencies, container images, Infrastructure as Code, and Kubernetes configurations before deployment.

---

# 📝 Summary

**Trivy** is a powerful, lightweight, and open-source security scanner that helps secure modern applications throughout the DevSecOps lifecycle. It detects vulnerabilities, misconfigurations, exposed secrets, and license issues across container images, filesystems, Infrastructure as Code, Kubernetes resources, and SBOMs. By integrating Trivy into CI/CD pipelines, organizations can identify security risks early, strengthen their software supply chain, and ensure only secure applications are deployed.

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