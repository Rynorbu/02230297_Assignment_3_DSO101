# Assignment 3: GitHub Actions CI/CD Pipeline - Final Report

## Overview
This assignment implemented a complete CI/CD (Continuous Integration/Continuous Deployment) pipeline using GitHub Actions to automatically build, test, and deploy a Docker application to Render.com.

---

## Steps Taken

### Step 1: Repository Setup
- ✅ Made GitHub repository **public** (required for DockerHub and Render access)
- ✅ Verified `package.json` has proper scripts (`start`, `build`, `test`)
- ✅ Confirmed Dockerfiles exist for both backend and frontend
- ✅ Updated all Dockerfiles to use **Node:20-alpine** (as per assignment requirements)

### Step 2: Docker Configuration
- ✅ Updated root `Dockerfile` to Node:20-alpine
- ✅ Updated `backend/Dockerfile` to Node:20-alpine
- ✅ Updated `frontend/Dockerfile` to:
  - Use multi-stage build (build stage + production stage)
  - Support dynamic PORT environment variable
  - Configure Nginx to serve React app
- ✅ Removed old `Jenkinsfile` (no longer needed)

### Step 3: GitHub Actions Workflow
- ✅ Created `.github/workflows/deploy.yml` with these steps:
  1. Checkout code from GitHub
  2. Set up Docker Buildx
  3. Login to DockerHub
  4. Build backend image
  5. Build frontend image
  6. Push backend image to DockerHub
  7. Push frontend image to DockerHub
  8. Trigger Render deployment webhooks

### Step 4: Docker Registry Setup
- ✅ Created DockerHub personal access token
- ✅ Pushed Docker images to DockerHub:
  - `rynorbu11/todo-app-backend:latest`
  - `rynorbu11/todo-app-frontend:latest`

### Step 5: GitHub Secrets Configuration
Added the following secrets to GitHub:
```
DOCKERHUB_USERNAME = rynorbu11
DOCKERHUB_TOKEN = [access token]
RENDER_BACKEND_WEBHOOK_URL = [webhook URL]
RENDER_FRONTEND_WEBHOOK_URL = [webhook URL]
DATABASE_URL = [PostgreSQL connection string]
```

### Step 6: Database Setup
- ✅ Created PostgreSQL database on Render.com
- ✅ Database credentials:
  - Host: `dpg-d7kms9u8bjmc73db1aug-a`
  - User: `taskflow_db_p3b4_user`
  - Port: 5432

### Step 7: Render Deployment
- ✅ Created Backend Web Service on Render
  - Image: `rynorbu11/todo-app-backend:latest`
  - Port: 5000
  - Environment variables configured (DB_HOST, DB_USER, DB_PASSWORD, etc.)
  
- ✅ Created Frontend Web Service on Render
  - Image: `rynorbu11/todo-app-frontend:latest`
  - Port: 3000
  - Environment variables configured (REACT_APP_API_URL)

---

## Challenges Faced

### Challenge 1: Frontend Dockerfile Port Issue ❌
**Problem:** Frontend container exposed port 80, but Render tried to use port 3000
**Solution:** Modified Dockerfile to dynamically set Nginx port based on `PORT` environment variable

### Challenge 2: GitHub Actions Workflow Syntax Errors ❌
**Problem:** Invalid `if` conditions in workflow file caused validation errors
**Examples:**
- ❌ `if: ${{ secrets.RENDER_BACKEND_WEBHOOK_URL != '' }}`
- ✅ Fixed with: `continue-on-error: true`

**Solution:** Simplified workflow conditions and used error handling instead

### Challenge 3: Database Connection Setup ❌
**Problem:** Initially unclear where to get DATABASE_URL and how to configure it
**Solution:** Extracted credentials from Render PostgreSQL service and configured individual environment variables for backend service

### Challenge 4: Image URL Format ❌
**Problem:** Confusion between DockerHub URL and image URL format
- DockerHub URL: `https://hub.docker.com/repository/docker/rynorbu11/todo-app-backend`
- Image URL for Render: `rynorbu11/todo-app-backend:latest`
**Solution:** Understood that Render auto-defaults to DockerHub registry

### Challenge 5: Frontend App Not Loading ❌
**Problem:** Frontend showed "Not Found" error when accessed
**Solution:** Fixed Dockerfile to properly handle PORT environment variable and configure Nginx

---

## Learning Outcomes

### 1. CI/CD Automation
- Learned how GitHub Actions automatically builds, tests, and deploys on every push
- Understood the importance of automated pipelines for consistency and reliability

### 2. Docker Best Practices
- **Multi-stage builds:** Separate build and production stages to reduce image size
- **Environment variables:** How to make containers configurable for different environments
- **Alpine images:** Benefits of using smaller base images (Node:20-alpine vs Node:20)

### 3. Secret Management
- Never hardcode credentials in code or Dockerfiles
- Always use repository secrets for sensitive data
- Secrets are injected at runtime by CI/CD systems

### 4. Infrastructure as Code (IaC)
- GitHub Actions workflows as code (`.yml` files)
- Configuration management through environment variables
- Benefits of version-controlling infrastructure changes

### 5. Deployment Workflow
- Build → Registry → Deployment cycle
- Webhook automation for automatic redeployment
- Health checks and service monitoring

### 6. Containerization Benefits
- Same container runs locally and in production
- No "it works on my machine" problems
- Easy scaling and replication

### 7. Networking & Configuration
- Internal vs External database URLs
- Frontend-backend communication setup
- Port mapping and environment-specific configuration

---

## Live Deployment Links

### Frontend Application
**URL:** https://todo-app-frontend-nuue.onrender.com

### Backend API
**Base URL:** https://taskflow-backend.onrender.com
**API Endpoints:** 
- GET `/api/todos` - Get all tasks
- POST `/api/todos` - Create new task
- PUT `/api/todos/:id` - Update task
- DELETE `/api/todos/:id` - Delete task

### Database
**Type:** PostgreSQL on Render
**Status:** Connected and running

---

## Evidence Screenshots

### 1. GitHub Repository (Public)
[Screenshot showing repository set to public]

### 2. GitHub Actions Workflow - Successful
[Screenshot showing all workflow steps completed with green checkmarks]

### 3. Docker Hub - Backend Image
[Screenshot showing `rynorbu11/todo-app-backend:latest` pushed to registry]

### 4. Docker Hub - Frontend Image
[Screenshot showing `rynorbu11/todo-app-frontend:latest` pushed to registry]

### 5. Render Backend Service - Live
[Screenshot showing backend service status: "Live"]

### 6. Render Frontend Service - Live
[Screenshot showing frontend service status: "Live"]

### 7. PostgreSQL Database on Render
[Screenshot showing database connection details]

### 8. Running Frontend Application
[Screenshot showing the todo app loaded at Render URL]

---

## Technologies Used

| Technology | Purpose | Version |
|-----------|---------|---------|
| GitHub | Source code hosting | - |
| GitHub Actions | CI/CD automation | Built-in |
| Docker | Containerization | Desktop |
| DockerHub | Container registry | Public |
| Node.js | Backend runtime | 20-alpine |
| React | Frontend framework | 18.2.0 |
| PostgreSQL | Database | 15 |
| Render | Cloud deployment | Free tier |
| Nginx | Reverse proxy / Web server | Alpine |

---

## Key Commands Used

```bash
# Build Docker images locally
docker build -t rynorbu11/todo-app-backend:latest ./backend
docker build -t rynorbu11/todo-app-frontend:latest ./frontend

# Push to DockerHub
docker login
docker push rynorbu11/todo-app-backend:latest
docker push rynorbu11/todo-app-frontend:latest

# Git commands
git add .
git commit -m "Setup GitHub Actions CI/CD pipeline"
git push origin main
```

---

## Conclusion

This assignment successfully demonstrated how to:
- ✅ Containerize a multi-tier application with Docker
- ✅ Automate CI/CD pipelines using GitHub Actions
- ✅ Manage secrets securely
- ✅ Deploy applications to production
- ✅ Set up databases and environment variables
- ✅ Implement webhook-based automatic redeployment

The entire pipeline is now automated: every push to the main branch triggers:
1. Docker image builds
2. Images pushed to DockerHub
3. Render services automatically redeploy
4. No manual intervention needed

---

## What I Learned Most

**The biggest learning:** Automation is powerful! Instead of manually building and deploying every change, the CI/CD pipeline handles it automatically. This saves time, reduces errors, and ensures consistency.

**Next Steps:** In the future, I could:
- Add automated testing in the GitHub Actions workflow
- Set up monitoring and alerting
- Implement staging environments for testing before production
- Use Kubernetes for advanced deployment scenarios
