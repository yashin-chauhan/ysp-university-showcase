# 🖥️ Product: Super Admin Governance Console

## 1. Overview

The Super Admin Console (`/admin`) serves as the administrative command center for university webmasters and registrars. Built on top of the responsive CoolAdmin theme, it provides complete control over institutional content, faculty moderation, and statutory publications.

---

## 2. Key Administrative Modules

### 2.1 Faculty Directory & Moderation Manager (`/admin/faculty`)
- **Faculty Roster:** Interactive table powered by DataTables 1.13 displaying ID, assigned page, names, email, phone, college, department, photo, and status.
- **Dynamic Page Mapping:** Dropdown selector to bind an approved faculty record to a specific college or department page slug (e.g. `cohft-facu`).
- **One-Click AJAX Status Toggle:** Instantly switches faculty between `Active` and `Deactivated` states without page reload.
- **Manual Faculty Registration (`/admin/faculty/add`):** Allows administrative personnel to onboard faculty profiles directly on their behalf.

---

### 2.2 Classified Notification & Tender Publisher (`/admin/notification/{url}`)
- Supports segregated publication feeds for:
  - `notification` (General University Circulars)
  - `farmer` (Farmer's Corner & Agro Advisories)
  - `links` (Important Links)
  - `tenders` (Procurement Tenders & RFPs)
  - `vacancy` / `employment` (Recruitment Notices)
  - `nirf` (NIRF Institutional Disclosures)
- Provides modal-based notice creation with PDF upload, external URL linking, and submission deadline specification (`last_date`).

---

### 2.3 Dynamic Course Matrix & Table Editor (`/admin/table/coh-course-table`)
- Enables academic administrators to manage course credit-hour tables for degree programs.
- Supports adding, editing, and updating course codes, course titles, and theory/practical credit splits (`3(2+1)`).

---

### 2.4 Dynamic Navigation Menu Manager (`/admin/navbar`)
- Direct interface to create and manage sub-navigation items for colleges and institutes.
- Associates links with categories (`cohft`, `basic-science`, etc.).
