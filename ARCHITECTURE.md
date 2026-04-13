# System Architecture (Offline + LAN)

## 📌 High-Level Architecture

```
[ User PC 1 ]       \
[ User PC 2 ]        --> Browser --> http://SERVER-IP:3000
[ User PC 3 ]       /

                ↓
        [ Local Server Machine ]
        ├── Backend (Node.js API)
        ├── Frontend (React build)
        ├── PostgreSQL Database
        └── File Storage (/storage)
```

---

## 🧠 Architecture Explanation

### 1. Local Server

* Hosts backend + database
* Acts as central system

### 2. Client Systems

* Access via browser
* No installation required

### 3. Communication

* HTTP over LAN network
* No internet dependency

---

## ⚙️ Tech Stack Rationale

| Layer      | Tech       | Reason     |
| ---------- | ---------- | ---------- |
| Frontend   | React      | Fast UI    |
| Backend    | Node.js    | Scalable   |
| Database   | PostgreSQL | Reliable   |
| Deployment | Docker     | Easy setup |

---

## 📌 Design Principles

* Offline-first
* Multi-user support
* Centralized data
* Future cloud-ready
