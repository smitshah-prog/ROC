# Deployment Guide (Offline + Future Cloud)

## 🖥️ Local Deployment (Primary)

### Step 1: Install Docker

Download Docker Desktop

---

### Step 2: Run Application

```bash
docker-compose up -d
```

---

### Step 3: Access System

```
http://<SERVER-IP>:3000
```

---

### Step 4: Configure Firewall

* Allow port 3000
* Allow PostgreSQL port (if needed)

---

## ☁️ Future Cloud Deployment (AWS)

### Services Required

* EC2 (Backend)
* RDS (PostgreSQL)
* S3 (Storage)

---

### Steps

1. Deploy backend on EC2
2. Migrate DB to RDS
3. Move storage to S3
4. Configure domain + SSL

---

## 📌 Backup Strategy

* Daily DB backup
* File storage backup

---

## 📌 Notes

* Keep same architecture → easy migration
