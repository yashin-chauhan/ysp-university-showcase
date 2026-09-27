# 👤 Product: Faculty Self-Service & Onboarding Portal

## 1. Overview

The Faculty Self-Service Portal (`/emp-register`, `/emp/login`, `/employee/profile`) provides university teaching staff, scientists, and researchers with an independent self-service workspace to maintain their academic records and credentials.

---

## 2. Key Features & User Capabilities

### 2.1 Two-Phase Onboarding with Domain Email & OTP
- Prospective faculty register at `/emp-register`.
- Enforces institutional email validation (`@tingebharat.com` / university pattern).
- Dispatches a 5-digit verification code to the applicant's inbox.
- Verifies the OTP asynchronously via AJAX before permitting password hashing and database insertion.

---

### 2.2 Profile & Research Credential Management (`/employee/profile`)
- **Biographical & Contact Information:** Name, official mobile number, fax number, and departmental email.
- **Institutional Affiliation:** Constituent college and academic department selection.
- **Academic Credentials:** Designation (Dean, Professor, Associate Professor, Assistant Professor, Scientist), academic discipline, and research specialization.
- **Vision Statement:** Research and teaching mission statement.
- **Document & Photo Uploads:** High-resolution profile avatar and updated curriculum vitae (PDF format).

---

### 2.3 Faculty Circulars & Internal Notices (`/employee/notification`)
- Access to internal faculty notifications, committee appointments, and academic board circulars.
- Automatic filtering of expired internal announcements.
