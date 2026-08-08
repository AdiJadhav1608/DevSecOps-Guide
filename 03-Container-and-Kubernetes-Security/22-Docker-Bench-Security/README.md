# 🛡️ Docker Bench Security

---

# 📖 Introduction

Docker containers provide a lightweight and portable way to run applications, but Docker environments must be configured securely to reduce the risk of attacks.

**Docker Bench for Security** is an open-source script developed by Docker that checks a Docker installation against security best practices based on the **CIS Docker Benchmark**.

It performs automated checks on areas such as:

- Docker daemon configuration
- Container configuration
- Docker images
- Container runtime
- Docker networking
- Logging
- File permissions
- Linux security settings

In DevSecOps, Docker Bench Security can be integrated into security processes to identify Docker configuration weaknesses before they become security risks.

> **"Secure the container environment, not just the application inside it."**

---

# 🎯 Objectives

After reading this guide, you will understand:

- What Docker Bench Security is
- What CIS Docker Benchmark means
- Why Docker security auditing is important
- Docker Bench architecture
- How to install Docker Bench
- How to run security checks
- How to understand the results
- Common Docker security checks
- CI/CD integration
- Best practices
- Interview questions

---

# 📖 What is Docker Bench Security?

**Docker Bench for Security** is a security auditing tool that checks whether a Docker environment follows recommended security practices from the **CIS Docker Benchmark**.

It is primarily a shell script that performs automated checks against:

```text
Docker Host
Docker Daemon
Docker Images
Containers
Docker Configuration
Docker Runtime
```

The tool produces warnings and recommendations for security issues that should be reviewed and remediated.

---

# 🔐 What is CIS Docker Benchmark?

The **CIS Docker Benchmark** is a set of security recommendations for securely configuring Docker.

CIS stands for:

**Center for Internet Security**

The benchmark provides security controls for areas such as:

- Host configuration
- Docker daemon configuration
- Docker daemon files
- Container images
- Container runtime
- Docker security operations

Docker Bench uses these recommendations as the basis for its checks.

---

# 🚀 Why Docker Bench Security is Important

Without security auditing:

- Docker configurations may remain insecure.
- Containers may run with unnecessary privileges.
- Docker daemon permissions may be too broad.
- Sensitive files may have incorrect permissions.
- Images may contain unnecessary components.
- Logging and monitoring may be inadequate.

Docker Bench helps organizations:

- Identify configuration weaknesses
- Improve Docker security
- Follow CIS recommendations
- Automate security auditing
- Strengthen container security
- Support DevSecOps compliance

---

# 🏗️ Docker Bench Security Architecture

```text
                 Docker Host
                      │
                      ▼
              Docker Bench Script
                      │
       ┌──────────────┼──────────────┐
       │              │              │
       ▼              ▼              ▼
 Docker Daemon     Containers      Images
       │              │              │
       └──────────────┼──────────────┘
                      ▼
               Security Checks
                      │
                      ▼
                Audit Results
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
       PASS / INFO              WARN
                                  │
                                  ▼
                           Remediation
```

---

# 🔍 Main Areas Checked

Docker Bench performs checks across several security areas.

```text
Docker Bench Security
│
├── Host Configuration
│
├── Docker Daemon Configuration
│
├── Docker Daemon Files
│
├── Container Images
│
├── Container Runtime
│
├── Docker Security Operations
│
└── Logging & Monitoring
```

---

# 1️⃣ Host Configuration

Docker Bench checks security-related settings on the underlying host.

Examples include:

- Linux kernel security
- Filesystem configuration
- User permissions
- Security modules
- Docker package version

### Why it matters

A compromised or poorly configured host can affect every container running on it.

---

# 2️⃣ Docker Daemon Configuration

The Docker daemon controls containers and images.

Docker Bench checks configurations such as:

- Docker daemon permissions
- Remote access
- TLS configuration
- User privileges
- Logging configuration

Example:

```bash
systemctl status docker
```

### Explanation

This command checks whether the Docker daemon is running.

---

# 3️⃣ Docker Daemon Files

Docker Bench checks permissions and ownership of important Docker files.

Examples:

```text
/etc/docker/
/var/lib/docker/
```

Check Docker directory:

```bash
ls -ld /etc/docker
```

Check Docker data directory:

```bash
ls -ld /var/lib/docker
```

### Why it matters

Incorrect permissions could allow unauthorized users to modify Docker configuration or access sensitive information.

---

# 4️⃣ Container Images

Docker Bench checks security-related properties of container images.

Examples:

- Trusted images
- Image vulnerabilities
- Unnecessary packages
- Image lifecycle
- Image ownership

For vulnerability scanning, tools such as Trivy should also be used.

```bash
trivy image nginx:latest
```

---

# 5️⃣ Container Runtime

Docker Bench checks running containers for security weaknesses.

Examples:

- Containers running as root
- Privileged containers
- Excessive Linux capabilities
- Host networking
- Host PID namespace
- Sensitive host directories mounted into containers

---

# ⚠️ Privileged Container Example

Avoid:

```bash
docker run --privileged ubuntu
```

A privileged container receives significantly elevated access to the host.

Prefer running containers with only the permissions they actually require.

---

# 👤 Running Containers as Non-Root

Check running containers:

```bash
docker ps
```

Inspect a container:

```bash
docker inspect mycontainer
```

A secure application should preferably run using a dedicated non-root user.

Example Dockerfile:

```dockerfile
FROM python:3.12-slim

# Create a dedicated application user
RUN useradd --create-home appuser

WORKDIR /app

COPY . .

# Run the application as a non-root user
USER appuser

CMD ["python", "app.py"]
```

---

# 🔒 Linux Capabilities

Linux capabilities divide traditional root privileges into smaller permissions.

Avoid giving unnecessary capabilities.

Example:

```bash
docker run \
  --cap-drop ALL \
  --cap-add NET_BIND_SERVICE \
  nginx
```

### Explanation

```text
--cap-drop ALL
```

Removes all Linux capabilities.

```text
--cap-add NET_BIND_SERVICE
```

Adds only the capability required for binding to privileged ports.

This follows the **Principle of Least Privilege**.

---

# 📦 Install Docker Bench Security

Clone the official repository:

```bash
git clone https://github.com/docker/docker-bench-security.git
```

Move into the directory:

```bash
cd docker-bench-security
```

Check the files:

```bash
ls
```

You should see files including:

```text
docker-bench-security.sh
README.md
functions/
tests/
```

---

# ▶️ Run Docker Bench Security

Execute:

```bash
sudo sh docker-bench-security.sh
```

Depending on the installation and environment, you may also run:

```bash
sudo ./docker-bench-security.sh
```

### Explanation

The script examines the Docker host and performs multiple security checks based on the CIS Docker Benchmark.

---

# 📊 Understanding Docker Bench Output

A typical result can contain:

```text
[PASS]   Docker daemon configuration
[WARN]   Docker daemon is not configured with TLS
[INFO]   Docker version information
[PASS]   Container logging configured
[WARN]   Container running as root
```

The results generally use categories such as:

```text
PASS
WARN
INFO
```

---

# 🟢 PASS

A **PASS** indicates that the tested security recommendation was satisfied.

Example:

```text
[PASS] Docker daemon configuration file permissions
```

---

# 🟡 WARN

A **WARN** indicates that a security recommendation was not satisfied or requires attention.

Example:

```text
[WARN] Docker daemon is not configured securely
```

Warnings should be reviewed and remediated where applicable.

---

# 🔵 INFO

An **INFO** message provides additional information about the environment or the security check.

Example:

```text
[INFO] Docker version: 27.x
```

---

# 🔄 Docker Bench Security Workflow

```text
Start Audit
     │
     ▼
Check Host
     │
     ▼
Check Docker Daemon
     │
     ▼
Check Docker Files
     │
     ▼
Check Images
     │
     ▼
Check Containers
     │
     ▼
Generate Results
     │
     ▼
Review WARN Results
     │
     ▼
Apply Remediation
     │
     ▼
Run Audit Again
```

---

# 🧪 Example Security Audit

Suppose Docker Bench reports:

```text
[WARN] Container is running as root

[WARN] Container has excessive capabilities

[WARN] Docker daemon remote access is insecure
```

The security team should investigate each finding.

Possible remediation:

```text
Running as root
        ↓
Create non-root user

Excessive capabilities
        ↓
Drop unnecessary capabilities

Insecure daemon access
        ↓
Restrict remote access
Use secure TLS configuration
```

---

# 🔐 Secure Docker Run Example

Instead of:

```bash
docker run --privileged myapp
```

Use a more restricted configuration:

```bash
docker run \
  --read-only \
  --cap-drop ALL \
  --security-opt no-new-privileges:true \
  myapp
```

### Explanation

```text
--read-only
```

Makes the container filesystem read-only.

```text
--cap-drop ALL
```

Removes unnecessary Linux capabilities.

```text
--security-opt no-new-privileges:true
```

Prevents processes from gaining additional privileges.

---

# ☁️ Docker Bench in DevSecOps

Docker Bench can be integrated into a DevSecOps workflow to audit the Docker environment.

```text
Developer
     │
     ▼
Git Push
     │
     ▼
CI/CD Pipeline
     │
     ├── Build Docker Image
     │
     ├── SAST
     │
     ├── Dependency Scan
     │
     ├── Trivy Image Scan
     │
     ├── Docker Bench Security
     │
     ▼
Security Validation
     │
     ├── PASS ──► Continue
     │
     └── WARN ──► Review / Fix
     │
     ▼
Container Registry
     │
     ▼
Deployment
```

---

# 🤖 Example CI/CD Security Stage

A simple Jenkins stage can run Docker Bench:

```groovy
stage('Docker Security Audit') {
    steps {
        sh '''
            git clone https://github.com/docker/docker-bench-security.git
            cd docker-bench-security
            sudo ./docker-bench-security.sh
        '''
    }
}
```

### Explanation

The pipeline:

1. Downloads Docker Bench.
2. Runs the security audit.
3. Generates security findings.
4. Allows the team to review configuration weaknesses.

For production pipelines, the script should be pinned to a reviewed version rather than blindly downloading the latest code during every build.

---

# 🆚 Docker Bench vs Trivy

| Docker Bench Security | Trivy |
|------------------------|-------|
| Audits Docker configuration | Scans vulnerabilities |
| Based on CIS Docker Benchmark | Uses vulnerability databases |
| Checks daemon configuration | Scans container images |
| Checks container configuration | Scans filesystems |
| Focuses on Docker environment | Also supports IaC, secrets and SBOMs |
| Security auditing | Vulnerability and misconfiguration scanning |

### Important

These tools are **not replacements for each other**.

A strong DevSecOps pipeline can use:

```text
Docker Bench
     +
Trivy
     +
SAST
     +
DAST
```

---

# 🆚 Docker Bench vs Container Image Scanning

```text
Docker Bench
     │
     ▼
"Is my Docker environment configured securely?"
```

```text
Container Image Scanner
     │
     ▼
"Does my container image contain vulnerabilities?"
```

Both questions are important for container security.

---

# 🚀 Docker Security Best Practices

- Use trusted base images.
- Keep Docker Engine updated.
- Scan images using Trivy or similar tools.
- Run containers as non-root users.
- Avoid privileged containers.
- Drop unnecessary Linux capabilities.
- Use read-only filesystems where possible.
- Restrict Docker socket access.
- Secure Docker daemon remote access.
- Use TLS for remote Docker administration.
- Avoid embedding secrets in images.
- Use resource limits.
- Monitor container activity.
- Regularly run Docker Bench Security.
- Follow CIS Docker Benchmark recommendations.

---

# 🔐 Docker Socket Security

The Docker socket is highly privileged.

Typical location:

```text
/var/run/docker.sock
```

Check its permissions:

```bash
ls -l /var/run/docker.sock
```

Avoid unnecessarily mounting it into containers:

```bash
docker run \
-v /var/run/docker.sock:/var/run/docker.sock \
myapp
```

### Why?

Access to the Docker socket can effectively provide powerful control over the Docker host.

Only trusted workloads should have access to it.

---

# 📈 Security Monitoring

Docker security should not stop after deployment.

Monitor:

- Container processes
- Docker daemon logs
- Authentication events
- Image changes
- Container creation
- Privileged containers
- Network activity
- Security alerts

Possible tools include:

- Docker logs
- CloudWatch
- Prometheus
- Grafana
- Falco
- SIEM platforms

---

# 🌍 Real-World Scenario

A company runs several production containers on an EC2 instance.

During a security audit, Docker Bench reports:

```text
[WARN] Container running with excessive privileges

[WARN] Docker daemon configuration requires improvement

[WARN] Sensitive Docker files have insecure permissions
```

The DevSecOps engineer:

```text
1. Reviews the warnings
        ↓
2. Removes unnecessary container privileges
        ↓
3. Corrects file permissions
        ↓
4. Secures Docker daemon configuration
        ↓
5. Runs Docker Bench again
        ↓
6. Verifies improved results
```

The environment is then subjected to additional image and runtime security testing.

---

# 📋 Docker Bench Security Checklist

| Security Control | Recommended |
|------------------|-------------|
| Docker host secured | ✅ |
| Docker Engine updated | ✅ |
| Docker daemon secured | ✅ |
| Docker files permissions reviewed | ✅ |
| Trusted images used | ✅ |
| Images scanned | ✅ |
| Containers run as non-root | ✅ |
| Privileged containers avoided | ✅ |
| Capabilities restricted | ✅ |
| Docker socket protected | ✅ |
| Resource limits configured | ✅ |
| Security auditing enabled | ✅ |
| Docker Bench regularly executed | ✅ |

---

# 🎤 Interview Questions

### 1. What is Docker Bench Security?

Docker Bench for Security is an automated auditing tool that checks Docker configurations against security recommendations from the CIS Docker Benchmark.

---

### 2. What is CIS Docker Benchmark?

The CIS Docker Benchmark is a set of security best practices for securely configuring Docker environments.

---

### 3. What does Docker Bench check?

It checks areas such as:

- Host configuration
- Docker daemon configuration
- Docker daemon files
- Container images
- Container runtime
- Docker security operations

---

### 4. What is the difference between Docker Bench and Trivy?

Docker Bench primarily audits the **Docker environment and configuration**, while Trivy primarily scans **images, filesystems, repositories, IaC, and other targets for vulnerabilities and security issues**.

---

### 5. Why should containers not run as root?

Running containers as non-root users follows the Principle of Least Privilege and limits the potential impact of a container compromise.

---

### 6. Why should privileged containers be avoided?

Privileged containers receive significantly elevated access to the host, increasing the impact of a potential container compromise.

---

### 7. What is the Docker socket?

The Docker socket, commonly located at:

```text
/var/run/docker.sock
```

is used to communicate with the Docker daemon. Access to it is highly privileged and should be carefully restricted.

---

### 8. How can Docker Bench be used in DevSecOps?

Docker Bench can be executed during security audits or CI/CD workflows to automatically identify Docker configuration weaknesses and verify compliance with security recommendations.

---

### 9. Is Docker Bench a vulnerability scanner?

Not primarily. Docker Bench is mainly a **configuration and security auditing tool** based on the CIS Docker Benchmark. Tools such as Trivy are better suited for vulnerability scanning.

---

### 10. What should you do after receiving a Docker Bench warning?

```text
Identify Finding
      ↓
Understand Risk
      ↓
Apply Remediation
      ↓
Run Docker Bench Again
      ↓
Verify Result
```

Not every warning should be blindly changed; configuration changes should be evaluated against application requirements and operational impact.

---

# 📝 Summary

**Docker Bench Security** is an important tool for auditing Docker environments against the **CIS Docker Benchmark**. It checks Docker host configuration, daemon settings, container configuration, image security practices, permissions, and other security controls.

In a DevSecOps environment, Docker Bench can be combined with tools such as **Trivy, SAST, DAST, and dependency scanners** to provide multiple layers of security throughout the container lifecycle.

A secure container environment requires more than scanning images—it also requires securely configuring the Docker host, daemon, containers, privileges, networking, and runtime.

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