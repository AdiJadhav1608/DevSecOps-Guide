# 🔐 Authentication vs Authorization

---

# 📖 Introduction

Authentication and Authorization are two fundamental concepts in **Cybersecurity**, **DevSecOps**, and **Cloud Computing**. Although they are often used together, they serve different purposes.

- **Authentication** answers the question: **"Who are you?"**
- **Authorization** answers the question: **"What are you allowed to do?"**

Every secure application, cloud platform, and enterprise system relies on these two security mechanisms to protect sensitive resources.

> **Authentication verifies identity, while Authorization determines permissions.**

---

# 🎯 Objectives

After reading this guide, you will understand:

- What Authentication is
- What Authorization is
- The differences between them
- Authentication methods
- Authorization models
- Real-world examples
- Best practices
- Interview questions

---

# 🏗️ Authentication and Authorization Flow

```text
            User
              │
              ▼
    Enter Username & Password
              │
              ▼
      Authentication
    (Verify Identity)
              │
      ✅ Success
              ▼
      Authorization
 (Check User Permissions)
              │
      ✅ Access Granted
              ▼
      Requested Resource
```

Authentication always happens **before** Authorization.

---

# 👤 What is Authentication?

## 📖 Definition

**Authentication** is the process of verifying the identity of a user, application, or device before granting access to a system.

It answers the question:

> **"Are you really who you claim to be?"**

---

## 🎯 Purpose

The purpose of Authentication is to ensure that only legitimate users can access the system.

---

## Common Authentication Methods

### 1️⃣ Username & Password

The most common authentication method.

Example:

```text
Username: aditya
Password: ********
```

---

### 2️⃣ Multi-Factor Authentication (MFA)

Requires two or more verification methods.

Example:

- Password
- OTP
- Fingerprint

---

### 3️⃣ Biometric Authentication

Uses unique biological characteristics.

Examples:

- Fingerprint
- Face Recognition
- Iris Scan

---

### 4️⃣ Token-Based Authentication

After login, the server generates an authentication token.

Examples:

- JWT (JSON Web Token)
- OAuth Tokens

---

### 5️⃣ Certificate-Based Authentication

Uses digital certificates instead of passwords.

Commonly used in:

- Enterprise networks
- VPNs
- Cloud services

---

# 🔑 What is Authorization?

## 📖 Definition

**Authorization** is the process of determining what an authenticated user is allowed to access or perform within a system.

It answers the question:

> **"What are you allowed to do?"**

---

## 🎯 Purpose

Authorization ensures users can only access resources and perform actions based on their assigned permissions.

---

## Examples

### Administrator

Can:

- Create users
- Delete users
- Modify configurations
- Access all resources

---

### Developer

Can:

- Deploy applications
- View logs
- Restart services

Cannot:

- Delete production databases

---

### Customer

Can:

- View profile
- Update password
- Place orders

Cannot:

- Access admin dashboard

---

# 🔄 Authentication vs Authorization

| Authentication | Authorization |
|---------------|---------------|
| Verifies identity | Determines permissions |
| Happens first | Happens after authentication |
| Confirms **who** you are | Determines **what** you can do |
| Uses passwords, OTP, biometrics | Uses roles and permissions |
| Login process | Access control process |

---

# 🛡️ Authorization Models

## 1️⃣ Role-Based Access Control (RBAC)

Permissions are assigned based on user roles.

Example:

| Role | Permission |
|------|------------|
| Admin | Full Access |
| Developer | Deploy Applications |
| Tester | Execute Test Cases |
| Viewer | Read Only |

---

## 2️⃣ Attribute-Based Access Control (ABAC)

Access decisions are based on user attributes such as:

- Department
- Location
- Time
- Device
- Job title

---

## 3️⃣ Policy-Based Access Control (PBAC)

Permissions are granted based on defined security policies.

Example:

```text
Allow access only during business hours.
```

---

# ☁️ Authentication and Authorization in AWS

### Authentication

AWS verifies the identity of a user using:

- IAM User
- IAM Role
- Access Keys
- AWS SSO

---

### Authorization

AWS IAM Policies determine:

- Which services can be accessed
- Which actions are allowed
- Which resources are permitted

Example IAM Policy

```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "*"
}
```

### Explanation

This policy allows the authenticated user to read objects from Amazon S3.

---

# 🛠️ Authentication Technologies

- Password Authentication
- Multi-Factor Authentication (MFA)
- OAuth 2.0
- OpenID Connect
- SAML
- JWT
- LDAP
- Active Directory

---

# 🛠️ Authorization Technologies

- AWS IAM
- Kubernetes RBAC
- Azure RBAC
- Linux File Permissions
- Database Privileges
- API Gateway Policies

---

# 🌍 Real-World Example

Imagine an online banking application.

### Step 1: Authentication

The user enters:

```text
Username
Password
OTP
```

The system verifies the identity.

✅ User successfully logs in.

---

### Step 2: Authorization

The banking application checks permissions.

The customer can:

- View account balance
- Transfer money
- Download statements

The customer cannot:

- View another customer's account
- Modify banking server settings
- Access administrator features

---

# 💻 Example: JWT Authentication

```text
User Login
      │
      ▼
Server verifies credentials
      │
      ▼
Generate JWT Token
      │
      ▼
Client stores token
      │
      ▼
Token sent with every request
      │
      ▼
Server validates token
      │
      ▼
Authorization checks
```

JWT enables stateless authentication for modern web applications and APIs.

---

# 🚀 Best Practices

## Authentication

- Use Multi-Factor Authentication (MFA).
- Enforce strong password policies.
- Store passwords using secure hashing algorithms.
- Implement account lockout after repeated failed login attempts.
- Use HTTPS for all authentication requests.

---

## Authorization

- Apply the Principle of Least Privilege (PoLP).
- Use Role-Based Access Control (RBAC).
- Regularly review user permissions.
- Remove unused accounts.
- Audit access logs frequently.

---

# ⚠️ Common Mistakes

- Using weak passwords
- Granting excessive permissions
- Sharing administrator accounts
- Storing passwords in plain text
- Missing Multi-Factor Authentication
- Hardcoding API keys in source code

---

# 📊 Authentication vs Authorization Summary

| Feature | Authentication | Authorization |
|----------|---------------|---------------|
| Purpose | Verify identity | Grant permissions |
| Question | Who are you? | What can you do? |
| Performed | Before login access | After successful authentication |
| Example | Password, OTP | IAM Policy, RBAC |
| Failure Result | Login denied | Access denied |

---

# 🎤 Interview Questions

### 1. What is Authentication?

Authentication is the process of verifying the identity of a user, application, or device before granting access.

---

### 2. What is Authorization?

Authorization determines what an authenticated user is allowed to access or perform.

---

### 3. What is the difference between Authentication and Authorization?

Authentication verifies identity, while Authorization determines permissions and access levels.

---

### 4. Which happens first: Authentication or Authorization?

Authentication always occurs before Authorization.

---

### 5. What is RBAC?

Role-Based Access Control (RBAC) is an authorization model where permissions are assigned based on user roles.

---

### 6. Give an AWS example of Authentication and Authorization.

- **Authentication:** AWS verifies an IAM User or IAM Role.
- **Authorization:** IAM Policies define which AWS resources and actions the authenticated identity can access.

---

# 📝 Summary

Authentication and Authorization are essential security mechanisms used to protect applications, cloud environments, and enterprise systems. Authentication verifies **who** the user is, while Authorization determines **what** that user is allowed to do. Together, they ensure that only trusted users can access the appropriate resources, making them a core part of every secure DevSecOps workflow.

---

# 🤝 Contribute

Contributions are welcome! Feel free to fork this repository, improve the content, and submit a pull request.

---

# 👨‍💻 Author


---