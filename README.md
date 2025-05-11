# Enhanced-container-security
# 🚀 Enhanced Container Security

This project simulates contemporary container attacks and implements a secure DevSecOps pipeline to detect and mitigate vulnerabilities using open-source security tools such as **Hadolint** and **Trivy**. A custom security application is developed and integrated into the CI/CD pipeline using **GitLab CI/CD**.

---

## 🧩 Project Overview

- **Objective**: Enhance container security by detecting vulnerabilities early in the development pipeline.
- **Scope**: 
  - Simulate real-world container threats.
  - Apply static analysis on Dockerfiles.
  - Perform vulnerability scanning on built container images.
  - Automate security checks using GitLab CI/CD.

---

## 🛠️ Technologies Used

| Category        | Tool/Technology          |
|----------------|---------------------------|
| CI/CD Pipeline | GitLab CI/CD              |
| Containerization | Docker                   |
| Security Tools | Trivy, Hadolint           |
| Scripting/Automation | Shell scripting       |

---

## ⚙️ CI/CD Pipeline Stages

### 1. `Lint`
- Tool: **Hadolint**
- Description: Performs static analysis on the Dockerfile to catch best-practice violations and potential issues.

### 2. `Scan`
- Tool: **Trivy**
- Description: Scans built Docker images for **HIGH** and **CRITICAL** vulnerabilities. If found, the pipeline fails.

### 3. `Build & Push`
- Builds the Docker image.
- Pushes the image to the GitLab Container Registry.

---

## 🧪 Vulnerability Scanning Logic

```bash
# Trivy scan command
trivy image --severity HIGH,CRITICAL --format table <image_name> > scan_report.txt

# Exit if critical vulnerabilities are found
if grep -q "CRITICAL\|HIGH" scan_report.txt; then
  echo "Vulnerabilities found."
  exit 1
fi
