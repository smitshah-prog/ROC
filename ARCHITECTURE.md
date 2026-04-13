# System Architecture

## 📌 High-Level Architecture

```
[ User Browser ]
        |
        v
[ React Frontend ]
        |
        v
[ Node.js Backend API ]
        |
        +-------------------+
        |                   |
        v                   v
[ PostgreSQL DB ]     [ External APIs ]
                      - OpenAI
                      - DSC/eSign
                      - Email/SMS
```

---

## 🧠 Architecture Explanation

### Frontend

* Handles UI/UX
* Communicates via REST API

### Backend

* Business logic
* Authentication
* Compliance engine

### Database

* Stores structured data
* JSON fields for flexible forms

### External Integrations

* AI for drafting
* DSC for signing

---

## ⚙️ Tech Stack Rationale

| Layer    | Technology | Reason            |
| -------- | ---------- | ----------------- |
| Frontend | React      | Fast, scalable UI |
| Backend  | Node.js    | High performance  |
| Database | PostgreSQL | Reliable & secure |
| Cloud    | AWS        | Scalable          |
| AI       | OpenAI     | Best LLM          |

---

## 📌 Design Principles

* Modular architecture
* API-first design
* Scalable & secure
