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

This project is designed as per Branch International’s DevOps take-home assignment.

---

# 📁 2. Project Structure

```
dummy-branch-ap/
│── app/
│    ├── routes/ (health, loans, stats)
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
│── Dockerfile
│── requirements.txt
│── README.md
```

---

# 🐳 3. Running Locally (Without Docker)

### **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

### **Install dependencies**
```bash
pip install -r requirements.txt
```

### **Run DB Migrations**
```bash
alembic upgrade head
```

### **Start Server**
```bash
export FLASK_APP=wsgi.py
flask run
```

---

# 🐳 4. Running with Docker (Development)

### **Command**
```bash
docker compose -f docker-compose.yml -f docker-compose.dev.yml up --build
```

### API will run at:
📌 http://localhost:5000

---

# 🗄️ 5. Database Seeding

Inside the running API container:

```bash
docker exec -it loan_api bash
python -m scripts.seed
```

---

# 🔥 6. Environment-Specific Deployments

### **DEV**
```
docker compose -f docker-compose.yml -f docker-compose.dev.yml up -d
```

### **STAGING**
```
docker compose -f docker-compose.yml -f docker-compose.staging.yml up -d
```

### **PRODUCTION**
```
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

---

# 🧪 7. API Endpoints

| Method | Endpoint           | Description             |
|--------|---------------------|-------------------------|
| GET    | `/health`           | Service health check    |
| GET    | `/api/loans`        | List all loans          |
| GET    | `/api/stats`        | Loan statistics summary |

---

# ⚙️ 8. CI/CD Pipeline (GitHub Actions)

📌 Workflow File: `.github/workflows/ci.yml`

CI pipeline performs:

✔ Checkout source code  
✔ Install dependencies  
✔ Run Alembic migrations  
✔ Build Docker image  
✔ Log in to GHCR  
✔ Push Docker image:  
```
ghcr.io/shekhawat2004/loan-api:latest
```

This image is used in **staging** and **production** Docker Compose files.

---

# 🏗️ 9. GHCR Docker Image

View the published image:

🔗 https://github.com/shekhawat2004?tab=packages

Package name: **loan-api**

---

# 🧱 10. Docker Compose – All Environments

### **Production**
`docker-compose.prod.yml`
- FLASK_ENV=production  
- POSTGRES_DB=loans_prod  
- Resource limits  
- Uses GHCR image

### **Staging**
`docker-compose.staging.yml`
- FLASK_ENV=staging  
- POSTGRES_DB=loans_staging  

### **Development**
`docker-compose.dev.yml`
- Uses local build  
- Debugging enabled  

---

# 📊 11. Sample API Output (After DB Seed)

### `/api/loans`
```json
[
  {
    "id": "...001",
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

# 🧑‍💻 12. Developer Info

**Author:** Aryan (shekhawat2004)  
**Role:** DevOps Engineer  
**Assignment:** Branch Microloan API

---

# 🎉 13. Conclusion

This complete project demonstrates:

✔ Docker & containerization  
✔ PostgreSQL + Alembic migrations  
✔ Multi-environment deployment  
✔ CI/CD automation  
✔ GitHub Container Registry (GHCR) integration  
✔ Clean REST API implementation  

This fulfills **100% of the Branch DevOps Take-Home Assignment requirements**.

