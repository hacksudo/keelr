# 🛡️ Keelr Docker Image Vulnerability SecureScanner
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
```

---

## 🚀 Quick Start & Deployment

### Prerequisites
- [Docker](https://docs.docker.com/get-docker/) (v20.10+)
- [Docker Compose](https://docs.docker.com/compose/) (v2.0+)

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/securescan.git
cd securescan
```

### 2. Configure Environment Variables
```bash
cp .env.example .env
```

### 3. Launch the Platform
```bash
docker compose up -d
```

### 4. Access the Dashboard
- **Web UI:** `http://localhost:3000`
- **Default Admin Login:**
  - **Username:** `admin@example.com`
  - **Password:** `admin123` *(Please change upon first login)*

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

## 📄 API & CLI Usage

### Trigger a Container Scan via cURL:
```bash
curl -X POST http://localhost:8000/api/v1/scan/docker \
  -H "Authorization: Bearer <YOUR_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{"image_name": "nginx:latest", "report_format": "pdf"}'
```

### Download Scan Report:
```bash
curl -X GET http://localhost:8000/api/v1/reports/<SCAN_ID>/download?format=pdf \
  -H "Authorization: Bearer <YOUR_TOKEN>" \
  --output report.pdf
```

---

## 🛑 Troubleshooting

### GitHub Image Upload Error: "Yowza, that’s a big file."
If you encounter this error while uploading screenshots or architecture diagrams to this repository via the GitHub web interface, it means your image exceeds GitHub's 25MB web upload limit.

**How to fix it:**
1. **Compress the Image (Recommended):** Use tools like [TinyPNG](https://tinypng.com/) or [Squoosh](https://squoosh.app/) to drastically reduce the file size.
2. **Convert the Format:** Change high-res raw files or PNGs to JPG or WebP.
3. **Push via Git CLI:** The command line allows uploading files up to 100MB.
   ```bash
   git add your-image-name.jpg
   git commit -m "Add large architecture diagram"
   git push origin main
   ```
4. **Host Externally:** Upload the image to an external host (Imgur, AWS S3) and embed it using markdown: `![Description](https://your-link.com/image.jpg)`

---

## 🛡️ License

This project is licensed under the **Apache-2.0 / MIT License** - see the [LICENSE](LICENSE) file for details.
