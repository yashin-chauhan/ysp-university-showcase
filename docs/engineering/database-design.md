# 💾 Engineering: Database Design & Asset Storage Architecture

## 1. Database Architecture Overview

The database utilizes **MySQL (InnoDB Engine)** to maintain relational integrity and transactional security.

---

## 2. Table Schemas & Specifications

### 2.1 `employees` Table
Stores faculty profiles, credentials, uploaded assets, and verification tokens.

| Column | Type | Nullable | Description |
|---|---|---|---|
| `id` | BIGINT UNSIGNED (PK) | No | Auto-increment primary key |
| `first_name` | VARCHAR(255) | No | Faculty first name |
| `middle_name` | VARCHAR(255) | Yes | Middle name |
| `last_name` | VARCHAR(255) | Yes | Last name / surname |
| `email` | VARCHAR(255) (UNIQUE) | No | Verified professional email |
| `phone` | VARCHAR(255) | Yes | Official contact telephone |
| `password` | VARCHAR(255) | No | Bcrypt hashed password |
| `college` | VARCHAR(255) | Yes | Constituent college name |
| `department` | VARCHAR(255) | Yes | Academic department |
| `designation` | VARCHAR(255) | Yes | Academic designation (Professor, Scientist, etc.) |
| `disciplice` | VARCHAR(255) | Yes | Academic discipline |
| `specialization` | VARCHAR(255) | Yes | Research specialization |
| `mission` | TEXT | Yes | Academic & research mission statement |
| `fax` | VARCHAR(255) | Yes | Departmental fax number |
| `image` | VARCHAR(255) | Yes | Stored filename of profile avatar |
| `docs` | VARCHAR(255) | Yes | Stored filename of CV / credential attachment |
| `page` | VARCHAR(255) | Yes | Target Blade page slug (e.g. `cohft-facu`) |
| `status` | INT | No (Def: 0) | Moderation status (1: Active, 0: Inactive) |
| `email_otp` | VARCHAR(255) | Yes | Verification OTP token |
| `created_at` / `updated_at` | TIMESTAMP | Yes | Timestamps |

---

### 2.2 `notification_links` Table
Stores classified circulars, tenders, job recruitments, and statutory NIRF reports.

| Column | Type | Nullable | Description |
|---|---|---|---|
| `id` | BIGINT UNSIGNED (PK) | No | Auto-increment primary key |
| `title` | VARCHAR(255) | No | Notice title / subject |
| `section` | VARCHAR(255) | No | Category (`tenders`, `vacancy`, `farmer`, `nirf`, `links`, etc.) |
| `type` | VARCHAR(255) | Yes | Delivery type (`pdf` or `url`) |
| `link` | VARCHAR(255) | Yes | External URL |
| `docs` | VARCHAR(255) | Yes | PDF document filename |
| `last_date` | DATE / VARCHAR | Yes | Submission deadline / auto-expiration date |
| `created_at` / `updated_at` | TIMESTAMP | Yes | Timestamps |

---

### 2.3 `navbar` Table
Maintains dynamic navigation links and campus menus.

| Column | Type | Nullable | Description |
|---|---|---|---|
| `id` | BIGINT UNSIGNED (PK) | No | Auto-increment primary key |
| `name` | VARCHAR(255) | No | Menu display label |
| `url` | VARCHAR(255) | No | Route path / view target |
| `type` | VARCHAR(255) | No | Category scope (`cohft`, `basic-science`, etc.) |
| `date` | TIMESTAMP | Yes | Creation timestamp |

---

### 2.4 `tables` Table
Maintains dynamic semester course lists and credit-hour tables.

| Column | Type | Nullable | Description |
|---|---|---|---|
| `id` | BIGINT UNSIGNED (PK) | No | Auto-increment primary key |
| `field_1` | VARCHAR(255) | Yes | Serial Number |
| `field_2` | VARCHAR(255) | Yes | Course Code / Subject Name |
| `field_3` | VARCHAR(255) | Yes | Course Title |
| `field_4` | VARCHAR(255) | Yes | Credit Hours (e.g. `3(2+1)`) |
| `created_at` / `updated_at` | TIMESTAMP | Yes | Timestamps |

---

## 3. Asset Storage Layout

Uploaded media and binary files are stored under Laravel's public storage directory (`storage/app/public/uploads`):

```
public/storage/uploads/
├── profile_images/    # Faculty profile photos (timestamp.ext)
├── emp_doc/           # Faculty curriculum vitae and documents (rand_timestamp.ext)
└── docs/              # Tender RFPs, circulars, and job application forms
```
