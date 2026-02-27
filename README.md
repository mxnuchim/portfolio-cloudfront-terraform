# 🌍 Production-Grade Portfolio Deployment on AWS with Terraform

### S3 + CloudFront + Secure Caching Architecture

<img width="1167" height="440" alt="Screenshot 2026-02-25 at 21 24 08" src="https://github.com/user-attachments/assets/5a50b876-6913-4d0a-a385-b5daefd1cefd" />

This repository contains the Terraform configuration used to provision and deploy my personal portfolio on AWS using a production-style architecture.

Rather than simply hosting static files, this project was designed to simulate real-world infrastructure decisions — focusing on security, performance, reproducibility, and global delivery.

---

# 🧠 Executive Summary

**Objective:**  
Design and deploy a globally distributed, secure, and cache-optimized static website using Infrastructure as Code.

**Outcome:**  
A fully reproducible AWS architecture leveraging S3, CloudFront, and Terraform with deliberate security controls and performance tuning.

**Core Principles Applied:**

- Infrastructure as Code (IaC)
- Least-privilege security
- Private origin architecture
- Intentional CDN caching strategy
- Idempotent deployments
- Production-grade design mindset

---

# 🏗 Architecture Overview

## High-Level Design

User → CloudFront (CDN) → Private S3 Origin

### Components

- **Amazon S3**
  - Private static site origin
  - Public access blocked
- **Amazon CloudFront**
  - Global CDN distribution
  - HTTPS enforced
  - Custom cache behaviors
- **Origin Access Control (OAC)**
  - Restricts S3 access to CloudFront only
- **IAM Policies**
  - Scoped permissions
  - No wildcard overexposure
- **Terraform**
  - Declarative infrastructure provisioning

---

# 🔐 Security Architecture

Security was implemented deliberately — not as an afterthought.

### Controls Implemented

- S3 bucket configured with **block public access**
- CloudFront Origin Access Control restricts direct origin access
- Bucket policy allows only CloudFront distribution ARN
- Viewer protocol policy enforces HTTPS
- No direct S3 website endpoint exposure
- IAM policies follow least-privilege principle

### Why This Matters

Many static portfolio deployments expose S3 publicly.  
This implementation prevents:

- Direct object enumeration
- Origin bypass
- Accidental public exposure
- Misconfigured ACL risks

The system behaves like a production static web deployment.

---

# ⚡ CDN & Caching Strategy

CloudFront behaviors were intentionally configured to balance performance and freshness.

| Path Pattern | TTL Strategy | Rationale                                  |
| ------------ | ------------ | ------------------------------------------ |
| `/assets/*`  | Long TTL     | Static files rarely change                 |
| `/*.html`    | Short TTL    | Content updates require faster propagation |
| Default      | Balanced     | Optimized general delivery                 |

### Design Goals

- Reduce origin load
- Minimize latency globally
- Improve cost efficiency
- Allow controlled invalidation patterns
- Demonstrate behavior-level tuning

Caching was treated as an architectural decision, not default configuration.

---

# 📦 Infrastructure as Code

All resources are provisioned using Terraform.

## Repository Structure

```

.
├── provider.tf
├── main.tf
├── variables.tf
├── outputs.tf
├── provider.tf
└── locals.tf

```

## IaC Design Philosophy

- No manual console configuration
- Idempotent execution
- Parameterized variables
- Clear separation of concerns
- Reproducible environments
- Predictable state management

Infrastructure can be destroyed and recreated reliably.

---

# 🚀 Deployment Workflow

### 1️⃣ Initialize

```bash
terraform init
```

### 2️⃣ Plan

```bash
terraform plan
```

### 3️⃣ Apply

```bash
terraform apply
```

### 4️⃣ Upload Build Artifacts

Deploy compiled static files to the provisioned S3 bucket.

### 5️⃣ Access Distribution

Access the site via the CloudFront domain output.

---

# 📈 Performance & Operational Considerations

### Edge Optimization

- Global edge caching
- Reduced latency
- Automatic content distribution

### Cost Awareness

- Optimized TTL settings reduce origin fetch frequency
- Static architecture minimizes compute costs

### Observability (Planned)

- CloudWatch metrics integration
- Access logging
- CDN monitoring dashboards

---

# 🔮 Future Enhancements

- Custom domain with ACM certificate
- CI/CD pipeline (GitHub Actions)
- Automated cache invalidation
- Multi-environment support (dev/staging/prod)
- WAF integration
- Terraform remote backend with state locking

---

# 🎯 What This Project Demonstrates

This project reflects:

- Architectural thinking over simple deployment
- Security-first cloud design
- Understanding of CDN internals
- Practical Terraform discipline
- Production-style static hosting patterns

It represents a transition from “deploying a website” to “designing infrastructure systems.”

---

# 📌 Conclusion

This portfolio deployment is intentionally over-engineered for a static site — by design.

The goal was not merely to host content, but to:

- Practice real-world infrastructure patterns
- Implement secure origin architecture
- Understand CloudFront caching deeply
- Apply Infrastructure as Code rigorously
- Think like a cloud engineer, not just a developer

The result is a secure, globally distributed, reproducible AWS deployment built with production-level intent.

```

```
