# 🛡️ SecureScan
> **All-in-One Centralized Container & Source Code Vulnerability Scanner with SBOM, Multi-Format Reporting, and Multi-User RBAC Management.**

---

## 📌 Overview

**SecureScan** is a centralized, self-hosted security platform engineered to simplify vulnerability management for modern DevSecOps teams. It allows organizations, administrators, and developers to automatically scan Docker container images and source code repositories, generate and audit Software Bills of Materials (SBOM), and produce exportable security reports in multiple formats.

With integrated **Role-Based Access Control (RBAC)**, administrators can manage user accounts, monitor scanning activity across teams, and enforce security policies from a single unified dashboard.

---

## ✨ Key Features

### 🐳 1. Docker & Container Security
- **Automated Image Scanning:** Scan local images, Docker Hub, AWS ECR, GCP GCR, and private registries.
- **Layer-by-Layer Vulnerability Detection:** Uncover OS package flaws (Debian, Alpine, RHEL, Ubuntu) and runtime dependencies.
- **Automated Triggers:** Schedule scans on a daily/weekly basis or trigger scans via webhooks and CI/CD pipelines.

### 📜 2. SBOM Generation & Vulnerability Auditing
- **Automated SBOM Creation:** Generate Software Bills of Materials in **SPDX** and **CycloneDX** standards.
- **Deep Dependency Tracking:** Identify hidden transitive dependencies and match them against known CVE databases (NVD, GitHub Advisories).

### 💻 3. Source Code Scanner (SAST & Secret Detection)
- **Static Code Analysis:** Scan source code repositories (Git, ZIP upload, local paths) for security vulnerabilities, code smells, and unsafe dependencies.
- **Hardcoded Secret Detection:** Detect leaked API keys, tokens, passwords, and private keys inside the codebase.

### 📊 4. Multi-Format Reporting Engine
Export detailed, executive, and technical audit reports with a single click:
- 📄 **PDF:** Executive summaries with charts, severity metrics (Critical, High, Medium, Low), and remediation tips.
- 🌐 **HTML:** Interactive, filterable browser-based reports.
- 📦 **JSON:** Machine-readable outputs for CI/CD integration and SIEM ingestion.
- 📝 **TXT:** Plaintext summaries for terminal logs and lightweight sharing.

### 👥 5. Multi-User Management & Admin Control (RBAC)
- **Centralized Dashboard:** Admins can oversee all scans performed across the entire organization.
- **User Lifecycle Management:** Admins can create, update, deactivate, and delete user accounts.
- **Audit Logs:** Track user actions, login timestamps, and scan execution history.
- **Isolated Workspaces:** Regular users can manage and review their own scan targets and reports.

### 🚀 6. Easy & Fast Deployment
- **Docker Compose Ready:** Spin up the entire platform (Web UI, API Backend, Worker Queue, Database) in one command.
- **Self-Hosted & Privacy-Focused:** All scans run on your own infrastructure; no source code or image data leaves your environment.

---

## 🏗️ Architecture & Core Engine Integration

```text
                 +-----------------------------------+
                 |           Web Dashboard           |
                 |      (Admin & User Portals)       |
                 +-----------------+-----------------+
                                   |
                                   v
                 +-----------------------------------+
                 |         REST API & Auth           |
                 |     (JWT / RBAC / User Mgmt)      |
                 +-----------------+-----------------+
                                   |
                  +----------------+----------------+
                  |                                 |
                  v                                 v
        +-------------------+             +-------------------+
        |  Container Engine |             | SAST/Code Engine  |
        |  (Trivy / Grype)  |             | (Semgrep / Syft)  |
        +---------+---------+             +---------+---------+
                  |                                 |
                  +----------------+----------------+
                                   |
                                   v
                 +-----------------------------------+
                 |       Reporting Engine            |
                 |    [ PDF | HTML | JSON | TXT ]    |
                 +-----------------------------------+
