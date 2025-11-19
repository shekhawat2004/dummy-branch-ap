# 🏦 Branch Microloan API – DevOps Take-Home Assignment  
A fully containerized Flask-based Loan API with PostgreSQL, Alembic migrations, CI/CD using GitHub Actions, and deployment-ready Docker Compose setups for **dev**, **staging**, and **production** environments.

---

## 🚀 1. Overview

This project implements a microloan service with:

- Flask REST API  
- PostgreSQL database  
- SQLAlchemy ORM  
- Alembic migrations  
- Environment-specific Docker Compose (Dev/Staging/Prod)  
- CI/CD pipeline that builds & pushes Docker images to **GitHub Container Registry (GHCR)**  

This project is designed as per **Branch International’s DevOps Take-Home Assignment**.

---

## 📁 2. Project Structure

```
dummy-branch-app/
│── app/
│    ├── routes/ (health, loans, stats, metrics)
│    ├── models.py
│    ├── schemas.py
│    ├── db.py
│    ├── config.py
│    └── __init__.py
│── scripts/
│    └── seed.py
│── alembic/
│── alembic.ini
│── docker-compose.yml
│── docker-compose.dev.yml
│── docker-compose.staging.yml
│── docker-compose.prod.yml
│── docker-compose.metrics.yml
│── prometheus.yml
│── Dockerfile
│── requirements.txt
│── nginx/
│      └── nginx.conf
│── certs/
│      ├── branchloans.crt
│      └── branchloans.key
│── README.md
```

---

## 🐳 3. Running Locally (Without Docker)

### **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate     # Windows → venv\Scripts\activate
```

### **Install dependencies**
```bash
pip install -r requirements.txt
```

### **Run DB migrations**
```bash
alembic upgrade head
```

### **Start the server**
```bash
export FLASK_APP=wsgi.py
flask run
```

---

## 🐳 4. Running with Docker (Development)

### **Start Dev Environment**
```bash
docker compose -f docker-compose.yml -f docker-compose.dev.yml up --build
```

### API will run at:
📌 http://localhost:5000

---

## 🗄️ 5. Database Seeding

Run inside API container:

```bash
docker exec -it loan_api bash
python -m scripts.seed
```

---

## 🔥 6. Environment-Specific Deployments

### **DEV**
```bash
docker compose -f docker-compose.yml -f docker-compose.dev.yml up -d
```

### **STAGING**
```bash
docker compose -f docker-compose.yml -f docker-compose.staging.yml up -d
```

### **PRODUCTION**
```bash
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

---

## 🧪 7. API Endpoints

| Method | Endpoint        | Description             |
|--------|------------------|-------------------------|
| GET    | `/health`        | Service health check    |
| GET    | `/api/loans`     | List all loans          |
| GET    | `/api/stats`     | Loan statistics summary |
| GET    | `/metrics`       | Prometheus metrics      |

---

## ⚙️ 8. CI/CD Pipeline (GitHub Actions)

📌 Workflow file: `.github/workflows/ci.yml`

CI pipeline performs:

✔ Checkout source code  
✔ Install dependencies  
✔ Run Alembic migrations  
✔ Build Docker image  
✔ Log in to GHCR  
✔ Push image →  
```
ghcr.io/shekhawat2004/loan-api:latest
```

This GHCR image is used in **staging** & **production**.

---

## 🏗️ 9. GHCR Docker Image

Published at:

🔗 https://github.com/shekhawat2004?tab=packages

Package Name → **loan-api**

---

## 🧱 10. Docker Compose – All Environments

### **Production**
- `FLASK_ENV=production`  
- `POSTGRES_DB=loans_prod`  
- Resource limits applied  
- Uses GHCR image  

### **Staging**
- `FLASK_ENV=staging`  
- `POSTGRES_DB=loans_staging`  

### **Development**
- Local build  
- Debug enabled  

---

## 📊 11. Sample API Output (After DB Seed)

### `/api/loans`
```json
[
  {
    "id": "loan_001",
    "borrower_id": "usr_kenya_001",
    "amount": "12500.00",
    "currency": "KES",
    "status": "pending"
  }
]
```

### `/api/stats`
```json
{
  "total_loans": 5,
  "total_amount": 124900,
  "avg_amount": 24980
}
```

---

## 📡 12. Monitoring (Prometheus + Grafana)

This project includes lightweight monitoring setup:

✔ `/metrics` endpoint using `prometheus-client`  
✔ Prometheus scrapes API metrics  
✔ Grafana dashboards for visualization  

### **Run monitoring stack**
```bash
docker compose -f docker-compose.yml \
  -f docker-compose.prod.yml \
  -f docker-compose.metrics.yml up -d
```

### **Access:**
- Prometheus → http://localhost:9090  
- Grafana → http://localhost:3000  
- Metrics → http://localhost:5000/metrics  

---

## 🧑‍💻 13. Developer Info

**Author:** Aryan Singh (shekhawat2004)  
**Role:** DevOps Engineer  
**Assignment:** Branch Loan API – Take-Home Project  

---

# 🎉 14. Conclusion

This project demonstrates:

✔ Docker & containerization  
✔ PostgreSQL + Alembic migrations  
✔ Multi-environment deployment  
✔ CI/CD automation (GitHub Actions)  
✔ GHCR image publishing  
✔ Monitoring (Prometheus + Grafana)  
✔ Clean REST API design  

This fulfills **100% of the Branch DevOps Take-Home Assignment requirements**.
