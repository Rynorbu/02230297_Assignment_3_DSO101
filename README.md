# Assignment 3: GitHub Actions CI/CD Pipeline & Docker Deployment

## Quick Links

- 🔗 **[FULL REPORT](./ASSIGNMENT_REPORT.md)** - Complete documentation with screenshots
- 🌐 **[Live Frontend](https://todo-app-frontend-nuue.onrender.com)** - Access the running app
- 📚 **[Backend API](https://taskflow-backend.onrender.com)** - API endpoints
- 🐳 **[DockerHub Images](https://hub.docker.com/u/rynorbu11)** - Container images

---

## Project Summary

This project implements a **complete CI/CD pipeline** that automates:
1. Building Docker containers for frontend and backend
2. Pushing images to DockerHub
3. Deploying to Render.com

**Everything is automated:** Push code → GitHub Actions builds → Images pushed → Auto-deployed! 🚀

---

## What's Included

```
├── backend/              # Node.js Express API
│   ├── server.js
│   ├── Dockerfile
│   └── package.json
├── frontend/             # React web app
│   ├── src/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── package.json
├── .github/workflows/    # GitHub Actions automation
│   └── deploy.yml
└── ASSIGNMENT_REPORT.md  # Full assignment report with evidence
```

---

## Quick Start (Local Development)

```bash
# Backend
cd backend
npm install
npm start    # Runs on port 5000

# Frontend (new terminal)
cd frontend
npm install
npm start    # Runs on port 3000
```

---

## CI/CD Pipeline Explained

```
Code Push to GitHub
        ↓
GitHub Actions Triggers
        ↓
Build Docker Images
        ↓
Push to DockerHub
        ↓
Render Webhook Triggered
        ↓
App Automatically Deployed ✅
```

---

## Technologies Used

- **CI/CD:** GitHub Actions
- **Containerization:** Docker & Docker Compose
- **Registry:** DockerHub
- **Deployment:** Render.com
- **Backend:** Node.js (Express)
- **Frontend:** React
- **Database:** PostgreSQL
- **Web Server:** Nginx

---

## Assignment Tasks Completed

- ✅ Verified GitHub repository is public
- ✅ Updated Dockerfiles to Node:20-alpine
- ✅ Created GitHub Actions workflow (`.github/workflows/deploy.yml`)
- ✅ Added GitHub Secrets for DockerHub credentials
- ✅ Pushed Docker images to DockerHub
- ✅ Created PostgreSQL database on Render
- ✅ Deployed backend service on Render
- ✅ Deployed frontend service on Render
- ✅ Configured automatic redeployment via webhooks
- ✅ Documented challenges and learning outcomes

---

## Key Features

🔄 **Automation:** Every push automatically builds and deploys
🔒 **Security:** Credentials stored as GitHub Secrets (never hardcoded)
📦 **Containerization:** Same container in dev and production
📈 **Scalability:** Easy to scale with container orchestration
🌍 **Cloud Ready:** Deployed on Render cloud platform

---

## Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Port conflicts | Modified Dockerfile to support PORT env variable |
| Workflow syntax errors | Simplified GitHub Actions with proper YAML syntax |
| Database connection | Extracted credentials from Render and configured separately |
| Image URL format | Used `username/image:tag` format for DockerHub |

---

## For Full Details

**See [ASSIGNMENT_REPORT.md](./ASSIGNMENT_REPORT.md) for:**
- Complete step-by-step guide
- All challenges faced and solutions
- Learning outcomes
- Screenshots as evidence
- Live deployment links

---

## Contact & Support

**Assignment 3 - DSO101**  
Due Date: As per course schedule  
Status: ✅ Completed

---

*Last Updated: April 23, 2026*