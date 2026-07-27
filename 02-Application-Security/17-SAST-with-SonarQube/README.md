# 🔒 SAST with SonarQube

---

# 📖 Introduction

Building secure applications requires identifying security vulnerabilities **before the application is deployed**. One of the most effective ways to achieve this is through **Static Application Security Testing (SAST)**.

**SonarQube** is one of the most popular tools for performing **SAST**, allowing developers to analyze source code without executing the application. It detects **bugs, security vulnerabilities, code smells, duplicated code, and maintainability issues**, enabling developers to fix problems early in the Software Development Life Cycle (SDLC).

In DevSecOps, SonarQube is commonly integrated into CI/CD pipelines to automate security and code quality checks for every commit or pull request.

> **"Find security vulnerabilities while writing code—not after deployment."**

---

# 🎯 Objectives

After reading this guide, you will understand:

- What SAST is
- Why SonarQube is used for SAST
- How SonarQube performs static analysis
- SonarQube architecture
- Setting up SonarQube
- Running SAST scans
- CI/CD integration
- Best practices
- Interview questions

---

# 📖 What is SAST?

**Static Application Security Testing (SAST)** is a testing technique that analyzes an application's **source code, bytecode, or binaries** without executing the application.

It helps identify security issues during development before software is deployed.

---

# 🔍 Why Use SonarQube for SAST?

SonarQube provides:

- Static code analysis
- Security vulnerability detection
- Bug detection
- Code smell identification
- Duplicate code detection
- Technical debt analysis
- Code coverage reports
- Quality Gate enforcement

---

# 🏗️ SAST with SonarQube Workflow

```text
Developer Writes Code
          │
          ▼
      Git Commit
          │
          ▼
     CI/CD Pipeline
          │
          ▼
    Sonar Scanner
          │
          ▼
   SonarQube Server
          │
          ▼
Static Code Analysis
          │
          ▼
Quality Gate Check
          │
     Pass?   Fail?
      │        │
      ▼        ▼
 Deploy     Fix Issues
```

---

# 🔐 What Can SonarQube Detect?

## 🐞 Bugs

Programming errors that may cause application failures.

Example:

```java
int a = 100;
int b = 0;

System.out.println(a / b);
```

### Explanation

Division by zero causes a runtime exception.

---

## 🔓 Security Vulnerabilities

Example:

```java
String query =
"SELECT * FROM users WHERE id='" + userInput + "'";
```

### Explanation

Concatenating user input directly into SQL queries can lead to **SQL Injection**.

---

## 🧹 Code Smells

Example:

```java
if(flag == true)
```

Better:

```java
if(flag)
```

---

## 📄 Duplicate Code

Repeated code blocks reduce maintainability and increase technical debt.

---

## ⚙️ Maintainability Issues

Examples:

- Long methods
- Complex logic
- Unused variables
- Dead code
- Nested conditions

---

# 🏛️ SonarQube Architecture

```text
Developer
     │
     ▼
Source Code
     │
     ▼
Sonar Scanner
     │
     ▼
SonarQube Server
     │
     ▼
Database
     │
     ▼
Web Dashboard
```

### Components

- **Sonar Scanner** – Scans the project.
- **SonarQube Server** – Performs analysis.
- **Database** – Stores reports and project history.
- **Dashboard** – Displays analysis results.

---

# 📊 Security Hotspots vs Vulnerabilities

| Vulnerabilities | Security Hotspots |
|-----------------|------------------|
| Confirmed security issues | Require manual review |
| Should be fixed immediately | Need developer verification |
| High security impact | Potential security concern |

---

# 🛠️ Install SonarQube Using Docker

```bash
# Pull SonarQube image
docker pull sonarqube:lts-community

# Run SonarQube container
docker run -d \
  --name sonarqube \
  -p 9000:9000 \
  sonarqube:lts-community
```

### Explanation

- Downloads the latest Community Edition image.
- Starts SonarQube.
- Opens the dashboard on **http://localhost:9000**.

Default login:

```text
Username : admin

Password : admin
```

---

# 💻 Install Sonar Scanner

Ubuntu:

```bash
# Download Sonar Scanner
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner.zip

# Extract files
unzip sonar-scanner.zip

# Verify installation
sonar-scanner --version
```

---

# 📄 Create Project Configuration

Create:

```text
sonar-project.properties
```

Example:

```properties
sonar.projectKey=demo-project
sonar.projectName=Demo Project
sonar.sources=src
sonar.host.url=http://localhost:9000
sonar.login=YOUR_TOKEN
```

### Explanation

- `projectKey` → Unique project identifier.
- `projectName` → Project name.
- `sources` → Source code directory.
- `host.url` → SonarQube server URL.
- `login` → Authentication token.

---

# 💻 Run a SAST Scan

```bash
# Analyze source code
sonar-scanner
```

### Explanation

The scanner:

- Reads project configuration.
- Uploads source code metadata.
- Performs static analysis.
- Detects bugs and vulnerabilities.
- Generates a quality report.

---

# 📊 Sample Analysis Report

```text
Bugs                : 3

Vulnerabilities     : 2

Code Smells         : 15

Duplications        : 1.2%

Coverage            : 82%

Quality Gate        : PASSED
```

---

# ☁️ SAST with Jenkins Pipeline

```groovy
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/example/project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Scan') {
            steps {
                sh 'sonar-scanner'
            }
        }
    }
}
```

### Explanation

- Downloads the project.
- Builds the application.
- Runs SonarQube static analysis.
- Generates a security report before deployment.

---

# ☁️ SAST in DevSecOps Pipeline

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
     ├── SonarQube SAST
     ├── Quality Gate
     ▼
Deploy to Test
     ▼
DAST & Container Scan
     ▼
Production
```

SAST is one of the earliest automated security checks in a DevSecOps pipeline.

---

# 🌍 Real-World Scenario

A developer commits new code that builds SQL queries using unsanitized user input.

↓

Jenkins starts the CI pipeline.

↓

SonarQube performs a SAST scan.

↓

It detects:

```text
SQL Injection Risk

Severity: High
```

↓

The Quality Gate fails.

↓

The deployment is blocked.

↓

The developer replaces the vulnerable code with prepared statements.

↓

A new scan passes successfully.

↓

The application is deployed securely.

---

# 🚀 Best Practices

- Run SAST on every commit or pull request.
- Enforce Quality Gates before deployment.
- Fix Critical and High vulnerabilities immediately.
- Review Security Hotspots regularly.
- Maintain high test coverage.
- Reduce code duplication.
- Keep SonarQube and rule sets updated.
- Integrate SAST into every CI/CD pipeline.

---

# 📊 SAST with SonarQube vs Manual Code Review

| SonarQube SAST | Manual Review |
|----------------|---------------|
| Automated | Human-driven |
| Fast | Slower |
| Continuous | Periodic |
| Detects common security issues | Better at business logic review |
| CI/CD Integration | Manual process |

Using both together provides the strongest security.

---

# 🎤 Interview Questions

### 1. What is SAST?

SAST (Static Application Security Testing) analyzes source code without executing the application to identify security vulnerabilities early in development.

---

### 2. Why is SonarQube used for SAST?

SonarQube automatically detects bugs, vulnerabilities, code smells, duplicate code, and maintainability issues before deployment.

---

### 3. Does SonarQube execute the application during analysis?

No. SonarQube performs **static analysis**, meaning it analyzes the source code without running the application.

---

### 4. What is a Quality Gate?

A Quality Gate is a set of predefined conditions that code must satisfy before it is considered ready for deployment.

---

### 5. What is the difference between a Vulnerability and a Security Hotspot?

A **Vulnerability** is a confirmed security issue that should be fixed, while a **Security Hotspot** is a potentially risky piece of code that requires manual review.

---

### 6. How is SonarQube integrated into DevSecOps?

SonarQube is integrated into CI/CD pipelines to automatically perform SAST scans, enforce Quality Gates, and prevent insecure code from reaching production.

---

# 📝 Summary

**SAST with SonarQube** enables organizations to detect security vulnerabilities, bugs, and code quality issues early in the development process. By integrating SonarQube into CI/CD pipelines, teams can automate static code analysis, enforce Quality Gates, reduce technical debt, and ensure that only secure, maintainable code is deployed to production. It is a fundamental practice in modern DevSecOps.

---

# 🤝 Contribute

Contributions are welcome! Feel free to fork this repository, improve the content, and submit a pull request.

---


---