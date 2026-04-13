# Data Model – ROC Compliance Software

## 📌 Overview

This system follows a **relational database design (PostgreSQL)** with normalized tables and selective use of JSON fields for flexibility.

Key principles:

* Multi-tenant (multiple clients)
* Audit-ready
* Event-driven compliance tracking
* Extensible for future modules (AI, MCA integration)

---

# 🧩 1. MASTER TABLES

## 👤 Users

Stores system users (CA firm staff)

| Field         | Type             | Description                   |
| ------------- | ---------------- | ----------------------------- |
| id            | UUID (PK)        | Unique user ID                |
| name          | VARCHAR          | Full name                     |
| email         | VARCHAR (unique) | Login email                   |
| password_hash | TEXT             | Encrypted password            |
| role          | ENUM             | Admin / Accountant / Approver |
| is_active     | BOOLEAN          | Active status                 |
| created_at    | TIMESTAMP        | Created time                  |
| updated_at    | TIMESTAMP        | Updated time                  |

---

## 🏢 Clients (Entities)

Represents Company / LLP

| Field              | Type      | Description                     |
| ------------------ | --------- | ------------------------------- |
| id                 | UUID (PK) | Unique client ID                |
| name               | VARCHAR   | Company name                    |
| entity_type        | ENUM      | Company / LLP                   |
| CIN                | VARCHAR   | Corporate Identification Number |
| LLPIN              | VARCHAR   | LLP Identification              |
| PAN                | VARCHAR   | PAN                             |
| TAN                | VARCHAR   | TAN                             |
| gstin              | VARCHAR   | GST (optional)                  |
| incorporation_date | DATE      | Incorporation date              |
| financial_year_end | DATE      | FY closing                      |
| registered_address | TEXT      | Address                         |
| email              | VARCHAR   | Official email                  |
| contact_no         | VARCHAR   | Contact                         |
| status             | ENUM      | Active / Closed                 |
| created_at         | TIMESTAMP | Created                         |
| updated_at         | TIMESTAMP | Updated                         |

---

## 👨‍💼 Directors / Partners

| Field            | Type         | Description |
| ---------------- | ------------ | ----------- |
| id               | UUID         |             |
| client_id        | FK → Clients |             |
| name             | VARCHAR      |             |
| DIN              | VARCHAR      |             |
| PAN              | VARCHAR      |             |
| designation      | VARCHAR      |             |
| appointment_date | DATE         |             |
| cessation_date   | DATE         |             |
| is_active        | BOOLEAN      |             |

---

## 👥 Shareholders / Partners

| Field            | Type    |
| ---------------- | ------- |
| id               | UUID    |
| client_id        | FK      |
| name             | VARCHAR |
| PAN              | VARCHAR |
| shares           | NUMERIC |
| share_percentage | NUMERIC |
| folio_no         | VARCHAR |
| certificate_no   | VARCHAR |

---

# 🧩 2. COMPLIANCE ENGINE TABLES

## 📅 ComplianceTypes (Master)

Defines all compliance types

| Field         | Type                   |
| ------------- | ---------------------- |
| id            | UUID                   |
| name          | VARCHAR (AOC-4, MGT-7) |
| applicable_to | ENUM                   |
| due_rule      | TEXT (logic or JSON)   |
| description   | TEXT                   |

---

## ⏰ ComplianceTasks

| Field              | Type                                 |
| ------------------ | ------------------------------------ |
| id                 | UUID                                 |
| client_id          | FK                                   |
| compliance_type_id | FK                                   |
| due_date           | DATE                                 |
| status             | ENUM (Pending / Completed / Overdue) |
| assigned_to        | FK Users                             |
| priority           | ENUM                                 |
| remarks            | TEXT                                 |
| completed_at       | TIMESTAMP                            |

---

## 🔔 ComplianceEvents (Trigger-based)

| Field        | Type                                   |
| ------------ | -------------------------------------- |
| id           | UUID                                   |
| client_id    | FK                                     |
| event_type   | ENUM (Director Change, Share Transfer) |
| event_date   | DATE                                   |
| triggered_by | FK Users                               |
| metadata     | JSON                                   |

👉 Used for automation:

* Add Director → trigger DIR-12
* Share transfer → trigger SH-4

---

# 🧩 3. MEETINGS & DOCUMENTS

## 📒 BoardMeetings

| Field            | Type                     |
| ---------------- | ------------------------ |
| id               | UUID                     |
| client_id        | FK                       |
| meeting_type     | ENUM (Board / AGM / EGM) |
| meeting_date     | DATE                     |
| venue            | TEXT                     |
| notice_sent_date | DATE                     |
| status           | ENUM                     |

---

## 🧾 Agendas

| Field       | Type    |
| ----------- | ------- |
| id          | UUID    |
| meeting_id  | FK      |
| title       | VARCHAR |
| description | TEXT    |
| sequence_no | INT     |

---

## 📝 Resolutions

| Field             | Type    |
| ----------------- | ------- |
| id                | UUID    |
| meeting_id        | FK      |
| resolution_type   | ENUM    |
| title             | VARCHAR |
| content           | TEXT    |
| section_reference | VARCHAR |
| passed            | BOOLEAN |

---

## 📄 Minutes

| Field       | Type     |
| ----------- | -------- |
| id          | UUID     |
| meeting_id  | FK       |
| content     | TEXT     |
| finalized   | BOOLEAN  |
| approved_by | FK Users |

---

# 🧩 4. REGISTERS MODULE

## 📚 Registers

| Field         | Type      |
| ------------- | --------- |
| id            | UUID      |
| client_id     | FK        |
| register_type | ENUM      |
| data          | JSONB     |
| last_updated  | TIMESTAMP |

👉 Types:

* Members Register
* Directors Register
* Charges Register
* Loans Register

---

# 🧩 5. ROC FORMS & FILINGS

## 📑 Filings

| Field            | Type    |
| ---------------- | ------- |
| id               | UUID    |
| client_id        | FK      |
| form_type        | VARCHAR |
| related_event_id | FK      |
| form_data        | JSONB   |
| status           | ENUM    |
| prepared_by      | FK      |
| approved_by      | FK      |
| filed_date       | DATE    |

---

## 📎 Attachments

| Field       | Type      |
| ----------- | --------- |
| id          | UUID      |
| client_id   | FK        |
| file_name   | VARCHAR   |
| file_path   | TEXT      |
| file_type   | VARCHAR   |
| uploaded_by | FK        |
| uploaded_at | TIMESTAMP |

---

# 🧩 6. WORKFLOW & APPROVAL

## 🔄 Workflows

| Field         | Type    |
| ------------- | ------- |
| id            | UUID    |
| module        | VARCHAR |
| step_name     | VARCHAR |
| sequence      | INT     |
| role_required | ENUM    |

---

## ✅ Approvals

| Field        | Type      |
| ------------ | --------- |
| id           | UUID      |
| reference_id | UUID      |
| module       | VARCHAR   |
| approved_by  | FK        |
| status       | ENUM      |
| remarks      | TEXT      |
| approved_at  | TIMESTAMP |

---

# 🧩 7. AUDIT & LOGGING

## 📜 AuditLogs

| Field     | Type      |
| --------- | --------- |
| id        | UUID      |
| user_id   | FK        |
| action    | VARCHAR   |
| module    | VARCHAR   |
| record_id | UUID      |
| old_value | JSON      |
| new_value | JSON      |
| timestamp | TIMESTAMP |

---

# 🧩 8. SYSTEM CONFIGURATION

## ⚙️ Settings

| Field | Type    |
| ----- | ------- |
| id    | UUID    |
| key   | VARCHAR |
| value | TEXT    |

---

## 🏷️ MasterLookups

| Field | Type    |
| ----- | ------- |
| id    | UUID    |
| type  | VARCHAR |
| value | VARCHAR |

---

# 🧩 9. FUTURE EXTENSIONS (READY DESIGN)

## 🤖 AI Prompts Log

| Field      | Type      |
| ---------- | --------- |
| id         | UUID      |
| module     | VARCHAR   |
| input      | TEXT      |
| output     | TEXT      |
| created_at | TIMESTAMP |

---

## ✍️ E-Sign Logs

| Field       | Type      |
| ----------- | --------- |
| id          | UUID      |
| document_id | FK        |
| signed_by   | FK        |
| provider    | VARCHAR   |
| status      | ENUM      |
| timestamp   | TIMESTAMP |

---

# 🔗 RELATIONSHIP SUMMARY

* Client → Directors (1:N)
* Client → Shareholders (1:N)
* Client → ComplianceTasks (1:N)
* Client → Meetings (1:N)
* Meeting → Resolutions (1:N)
* Meeting → Minutes (1:1)
* Client → Filings (1:N)

---

# ⚠️ DESIGN CONSIDERATIONS

## 1. Multi-user handling

* Use row-level locking
* Track updated_at

## 2. JSON Usage

* Flexible forms
* Avoid schema changes

## 3. Audit Requirement

* Every critical change logged

## 4. Scalability

* Ready for cloud migration

---

# ✅ FINAL NOTE

This data model supports:
✔ Full ROC lifecycle
✔ Automation-ready workflows
✔ AI integration
✔ Multi-user LAN system

👉 This is **enterprise-grade design** — you can directly build on this.
