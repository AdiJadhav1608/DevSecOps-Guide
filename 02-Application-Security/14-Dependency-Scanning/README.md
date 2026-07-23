# 📦 Dependency Scanning

---

# 📖 Introduction

Modern software development heavily relies on **open-source libraries, frameworks, packages, and third-party dependencies**. Instead of writing every feature from scratch, developers use existing components to speed up development.

While this improves productivity, it also introduces security risks. If a dependency contains a known vulnerability, every application using that dependency may become vulnerable.

**Dependency Scanning** is the process of automatically identifying software dependencies and checking them against known vulnerability databases such as the **National Vulnerability Database (NVD)** and **CVE (Common Vulnerabilities and Exposures)**.

In DevSecOps, dependency scanning is an essential security practice that helps detect vulnerable libraries early in the Software Development Life Cycle (SDLC).

> **"Most modern applications are only as secure as the libraries they depend on."**

---

# 🎯 Objectives

After reading this guide, you will understand:

- What Dependency Scanning is
- Why it is important
- How Dependency Scanning works
- Types of dependencies
- Popular scanning tools
- DevSecOps integration
- Best practices
- Interview questions

---

# 📖 What is Dependency Scanning?

**Dependency Scanning** is the automated process of identifying third-party software components used in an application and checking them for known security vulnerabilities.

It helps answer questions such as:

- Which libraries are being used?
- Are they up to date?
- Do they contain known CVEs?
- What is the severity of those vulnerabilities?
- Which dependencies should be updated?

---

# 🏗️ Why is Dependency Scanning Important?

Modern applications often include hundreds of dependencies.

Without Dependency Scanning:

- Vulnerable libraries remain unnoticed.
- Applications inherit known security flaws.
- Software supply chain attacks become more likely.
- Compliance becomes difficult.
- Security patches may be delayed.

With Dependency Scanning:

- Vulnerable packages are detected early.
- Critical CVEs are identified quickly.
- Security risks are reduced.
- Software remains up to date.
- DevSecOps automation is improved.

---

# 🔄 How Dependency Scanning Works

```text
Application Source Code
           │
           ▼
Read Dependency Files
(package.json, pom.xml, requirements.txt)
           │
           ▼
Identify Libraries & Versions
           │
           ▼
Compare with CVE Database
           │
           ▼
Generate Vulnerability Report
           │
           ▼
Update Vulnerable Dependencies
```

---

# 📦 Common Dependency Files

| Programming Language | Dependency File |
|----------------------|-----------------|
| Java | pom.xml |
| Maven | pom.xml |
| Gradle | build.gradle |
| Node.js | package.json |
| Python | requirements.txt |
| Go | go.mod |
| .NET | packages.config |
| PHP | composer.json |

---

# ⚠️ Common Dependency Risks

## 1️⃣ Outdated Libraries

Using old versions that contain publicly known vulnerabilities.

Example:

```text
Log4j 2.14.1
```

Affected by:

```text
CVE-2021-44228 (Log4Shell)
```

---

## 2️⃣ Malicious Packages

Attackers publish fake packages that imitate legitimate ones.

Example:

```text
expresss
```

instead of

```text
express
```

This attack is known as **Typosquatting**.

---

## 3️⃣ Dependency Confusion

Attackers publish malicious public packages with names matching internal packages, causing build systems to download the attacker's package instead.

---

## 4️⃣ Unmaintained Libraries

Dependencies that are no longer updated or supported may contain unresolved security vulnerabilities.

---

# 🛠️ Popular Dependency Scanning Tools

| Tool | Purpose |
|------|----------|
| OWASP Dependency-Check | Scan project dependencies |
| Trivy | Dependency & Container Scanning |
| Snyk | Dependency Vulnerability Detection |
| GitHub Dependabot | Automatic Dependency Updates |
| GitLab Dependency Scanning | CI/CD Security |
| Mend (WhiteSource) | Open Source Security |
| Grype | Package Vulnerability Scanner |

---

# 💻 Example 1: Scan Dependencies with Trivy

```bash
# Scan the current project
trivy fs .
```

### Explanation

- Scans the project directory.
- Detects installed packages.
- Compares package versions with vulnerability databases.
- Displays CVEs and severity levels.

---

# 💻 Example 2: OWASP Dependency-Check

```bash
# Scan the current project
dependency-check.sh --scan .
```

### Explanation

- Identifies project dependencies.
- Checks against the National Vulnerability Database (NVD).
- Generates an HTML security report.

---

# 💻 Example 3: GitHub Dependabot

A sample configuration file:

```yaml
version: 2

updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
```

### Explanation

- Checks project dependencies every week.
- Creates pull requests for updates.
- Helps keep dependencies secure and up to date.

---

# ☁️ Dependency Scanning in DevSecOps

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
      ├── Secret Scan
      ├── Dependency Scan
      ├── IaC Scan
      ├── Container Scan
      ▼
Deploy
      ▼
Continuous Monitoring
```

Dependency scanning is automatically performed before deployment.

---

# 🌍 Real-World Scenario

A developer adds an outdated open-source logging library to an application.

↓

The CI/CD pipeline runs a dependency scan.

↓

The scanner detects:

```text
CVE-2021-44228

Severity: Critical
```

↓

The pipeline fails the build.

↓

The developer upgrades the library to a secure version.

↓

A new scan confirms that the vulnerability has been resolved.

↓

The application is safely deployed.

---

# 🚀 Benefits of Dependency Scanning

- Detects known vulnerabilities early.
- Reduces software supply chain risks.
- Improves software quality.
- Supports compliance requirements.
- Automates security checks.
- Helps maintain updated dependencies.
- Integrates seamlessly with CI/CD pipelines.

---

# 💡 Best Practices

- Scan dependencies on every build.
- Keep libraries updated.
- Remove unused dependencies.
- Enable automated dependency updates.
- Review vulnerability reports regularly.
- Prioritize fixes using CVSS scores.
- Generate an SBOM for every release.
- Use trusted package repositories only.
- Monitor newly published CVEs.

---

# 📊 Dependency Scanning vs Container Scanning

| Dependency Scanning | Container Scanning |
|---------------------|-------------------|
| Scans application libraries | Scans Docker/container images |
| Focuses on package vulnerabilities | Focuses on OS packages and image layers |
| Uses dependency files | Uses container images |
| Detects vulnerable libraries | Detects vulnerable operating system packages and image components |

---

# 🎤 Interview Questions

### 1. What is Dependency Scanning?

Dependency Scanning is the process of identifying third-party libraries used in an application and checking them for known security vulnerabilities.

---

### 2. Why is Dependency Scanning important?

It helps detect vulnerable libraries before deployment, reducing software supply chain risks and improving application security.

---

### 3. Name some Dependency Scanning tools.

- Trivy
- OWASP Dependency-Check
- Snyk
- GitHub Dependabot
- Grype
- Mend (WhiteSource)

---

### 4. What is Dependency Confusion?

Dependency Confusion is an attack where malicious public packages with names matching internal packages are published, causing build systems to install the attacker's package.

---

### 5. What is Typosquatting?

Typosquatting is an attack where attackers publish packages with names similar to popular libraries, hoping developers accidentally install them.

---

### 6. How is Dependency Scanning integrated into DevSecOps?

Dependency Scanning is automated within CI/CD pipelines, allowing vulnerable libraries to be detected and updated before applications are deployed.

---

# 📝 Summary

Dependency Scanning is a critical DevSecOps practice that identifies vulnerable third-party libraries before they become security risks. By comparing project dependencies against trusted vulnerability databases such as CVE and NVD, organizations can quickly detect outdated or insecure packages, automate remediation, strengthen software supply chain security, and deliver more secure applications.

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