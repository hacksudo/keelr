# 🛡️ Keelr Docker Image Vulnerability SecureScanner
> **All-in-One Centralized Container & Source Code Vulnerability Scanner with SBOM, Multi-Format Reporting, and Multi-User RBAC Management.**

---

## 📌 Overview

**KeelrSecureScan** is a centralized, self-hosted security platform engineered to simplify vulnerability management for modern DevSecOps teams. It allows organizations, administrators, and developers to automatically scan Docker container images and source code repositories, generate and audit Software Bills of Materials (SBOM), and produce exportable security reports in multiple formats.

With integrated **Role-Based Access Control (RBAC)**, administrators can manage user accounts, monitor scanning activity across teams, and enforce security policies from a single unified dashboard.

<img width="2500" height="1464" alt="image" src="https://github.com/user-attachments/assets/2e9239fd-50c2-43c3-be33-0dadfb680f89" />


---

## ✨ Key Features

### 🐳 1. Docker & Container Security
- **Automated Image Scanning:** Scan local images, Docker Hub, AWS ECR, GCP GCR, and private registries.
- **Layer-by-Layer Vulnerability Detection:** Uncover OS package flaws (Debian, Alpine, RHEL, Ubuntu) and runtime dependencies.
- **Automated Triggers:** Schedule scans on a daily/weekly basis or trigger scans via webhooks and CI/CD pipelines.
  
  <img width="2500" height="1468" alt="image" src="https://github.com/user-attachments/assets/680d0e3d-f6dc-4cab-a2a4-9ec347dc4343" />


### 📜 2. SBOM Generation & Vulnerability Auditing
- **Automated SBOM Creation:** Generate Software Bills of Materials in **SPDX** and **CycloneDX** standards.
- **Deep Dependency Tracking:** Identify hidden transitive dependencies and match them against known CVE databases (NVD, GitHub Advisories).
- 
<img width="2500" height="1414" alt="image" src="https://github.com/user-attachments/assets/a647840a-423c-48a5-b38d-81eba444e7d7" />


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
```

---

## 🚀 Quick Start & Deployment

### Prerequisites
- [Docker](https://docs.docker.com/get-docker/) (v20.10+)
- [Docker Compose](https://docs.docker.com/compose/) (v2.0+)

### 1. Clone the Repository
```bash
git clone https://github.com/hacksudo/keelr.git
cd keelr
```

### 2. Configure Environment Variables
```bash
unzip keelr_scanner_login_v1.0.6.zip
cd keelr_scanner_login_v1.0.6
bash install.sh
```
or 
### 3. Launch the Platform
```bash
unzip keelr_scanner_login_v1.0.6.zip
cd keelr_scanner_login_v1.0.6
docker load keelr-scanner.tar
```

### 4. Access the Dashboard
- **Web UI:** `http://localhost:3001`
- **Default Admin Login:**
  - **Username:** `admin`
  - **Password:** `Admin@123` *(Please change upon first login)*

---

## 🛠️ User Roles & Permissions

| Feature / Action | Admin | Standard User |
| :--- | :---: | :---: |
| Run Docker Image Scans | ✅ | ✅ |
| Run Source Code Scans | ✅ | ✅ |
| Generate SBOM & Reports (PDF/HTML/JSON/TXT) | ✅ | ✅ |
| View Own Scan History | ✅ | ✅ |
| View Global Activity & All Users' Reports | ✅ | ❌ |
| Create & Delete User Accounts | ✅ | ❌ |
| Manage System Configuration & Integrations | ✅ | ❌ |

---


## 🛡️ License

This project is licensed under the **Apache-2.0 / MIT License** - see the [LICENSE](LICENSE) file for details.
