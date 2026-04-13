# ROC Compliance Software (Offline + LAN Based)

## 📌 Overview

This is an **offline-first ROC Compliance Management Software** designed for Chartered Accountants and professionals.

The system runs on a **local server (within office LAN)** and allows multiple users to access it through browser.

---

## 🎯 Key Features

* Client & Company Management
* Compliance Calendar & Tracking
* Board Resolution Generator
* Minutes & Registers Management
* Multi-user workflow (LAN based)
* Document storage (local server)
* Audit logs

---

## 🏗️ Architecture Type

* Offline-first (LAN-based)
* Centralized server system
* Browser-based access

---

## 🚀 Tech Stack

* Frontend: React
* Backend: Node.js (Express)
* Database: PostgreSQL
* Deployment: Docker (local server)

---

## ⚙️ Setup Instructions

### 1. Install Prerequisites

* Docker Desktop (Recommended)
* OR Node.js + PostgreSQL

---

### 2. Clone Repository

```bash
git clone https://github.com/your-repo/roc-compliance.git
cd roc-compliance
```

---

### 3. Run using Docker

```bash
docker-compose up -d
```

---

### 4. Access Application

From any system in LAN:

```bash
http://<SERVER-IP>:3000
```

Example:

```bash
http://192.168.1.10:3000
```

---

## 🔐 Default Login

* Email: [admin@local.com](mailto:admin@local.com)
* Password: Admin123

---

## 📁 Storage

All documents are stored locally in:

```
/storage/
```

---

## 📌 Future Upgrade

* Cloud deployment (AWS)
* AI-based drafting
* DSC integration
