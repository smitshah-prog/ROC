# ROC

# ROC Compliance SaaS

## 📌 Overview

ROC Compliance SaaS is a web-based platform designed for Chartered Accountants and Company Secretaries to manage corporate compliance efficiently.

The system helps in:

* Managing companies, directors, and shareholders
* Tracking compliance deadlines (ROC filings, AGM, etc.)
* Generating resolutions, minutes, and forms
* Managing workflows (maker-checker)
* Digital signing (DSC/eSign)
* AI-based drafting of documents

---

## 🚀 Tech Stack

* Frontend: React / Next.js
* Backend: Node.js (Express)
* Database: PostgreSQL
* Cloud: AWS
* AI: OpenAI API
* Storage: AWS S3

---

## ⚙️ Setup Instructions

### 1. Clone Repository

```bash
git clone https://github.com/your-repo/roc-compliance.git
cd roc-compliance
```

### 2. Backend Setup

```bash
cd backend
npm install
cp .env.example .env
npm run dev
```

### 3. Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

### 4. Database Setup

* Install PostgreSQL
* Create database: `roc_compliance`
* Run migrations:

```bash
npm run migrate
```

---

## 🔐 Environment Variables

Create `.env` file:

```
DB_URI=postgresql://user:password@localhost:5432/roc_compliance
JWT_SECRET=your_secret
OPENAI_API_KEY=your_key
AWS_ACCESS_KEY=xxx
AWS_SECRET=xxx
```

---

## 📦 Features (MVP)

* Company Management
* Compliance Calendar
* Document Storage
* Basic Registers
* User Roles

---

## 📌 Future Scope

* E-form automation
* AI drafting
* DSC integration
* Analytics dashboard
