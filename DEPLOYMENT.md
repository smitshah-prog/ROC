# Deployment Guide

## ☁️ Cloud Setup (AWS)

### 1. Create Services

* EC2 (Backend)
* RDS (PostgreSQL)
* S3 (Storage)
* CloudFront (CDN)

---

### 2. Backend Deployment

```bash
docker build -t roc-backend .
docker run -d -p 5000:5000 roc-backend
```

---

### 3. Frontend Deployment

* Use Vercel or AWS Amplify

---

### 4. Database Setup

* Create RDS instance
* Configure security groups

---

### 5. Environment Variables

Set in AWS:

* DB_URI
* JWT_SECRET
* API keys

---

### 6. CI/CD Pipeline

* GitHub Actions:

  * Build
  * Test
  * Deploy

---

### 7. Domain Setup

* Route53 / GoDaddy
* SSL via AWS Certificate Manager

---

## 📌 Monitoring

* CloudWatch logs
* Error tracking (Sentry)
