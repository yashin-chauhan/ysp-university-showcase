# 📸 Dr. YSP University — Screenshots & Interface Previews

This directory catalogs the user interface previews, architectural flows, and administrative console views of the YSP University platform ([https://uhf.ac.in/](https://uhf.ac.in/)).

---

## 🖥️ Public Institutional Portal

### 1. University Landing Page
- Modern university hero header with multi-tiered navigation (About Us, Admissions, Academics, Research, Extension Education, Resources, Tenders, Vacancies, NIRF).
- Dynamic sliding ticker for recent academic and administrative notices.
- Direct quick links for Students, Alumni, Library, Farmers, Virtual Tour, Linkages & MOUs.

### 2. Multi-College Department & Faculty Roster
- College of Horticulture and Forestry subpages (e.g. Thunag campus `cohft-facu`).
- Clean grid presentation of faculty members: full name, designation, college, official telephone, fax, email, and high-resolution profile photo.
- Dynamic rendering powered by `getFaculty($page)` helper.

### 3. Centralized Procurement Tenders & Job Vacancies
- Clean tabular view of active tenders and job recruitments.
- Dynamic date-filtered list preventing expired notices from displaying.
- Instant PDF download links for official tender specifications and application forms.

---

## 👨‍🏫 Faculty Self-Service Portal

### 1. Asynchronous Email Verification & OTP Onboarding (`/emp-register`)
- Clean, responsive registration form with institutional email verification.
- Two-step interactive OTP button flow with live Toastr notification toasts.

### 2. Faculty Profile Management Console (`/employee/profile`)
- Form to edit biographical data, academic discipline, research specialization, and mission statement.
- Avatar and curriculum vitae document upload dropzones.

---

## 🏢 Super Admin Governance Console

### 1. Central Administrative Faculty Management (`/admin/faculty`)
- Integrated DataTables view with multi-column sorting and live search.
- Dynamic page dropdown mapping to link faculty to specific departmental templates.
- One-click AJAX button toggling for Active / Deactivate states.

### 2. Classified Notice & Tender Publisher (`/admin/notification/{url}`)
- Modal-based upload interface with section tagging, external URL linking, PDF attachment, and `last_date` calendar picker.

### 3. Dynamic Academic Course Table Manager (`/admin/table/coh-course-table`)
- Inline table CRUD enabling administrators to add, edit, and update semester course matrices and credit hours.
