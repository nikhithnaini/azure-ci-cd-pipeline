# Azure DevOps Pipeline for Deploying a Dockerized App to Azure App Service

This Azure DevOps pipeline automates:
- Running unit and integration tests
- Building and pushing a Docker image to Azure Container Registry (ACR)
- Deploying the image to a **staging slot** in Azure App Service
- Performing health checks on the **staging slot**
- Swapping the staging slot to **production**
- Performing final health checks on **production**

---

## 📂 Pipeline Stages

1️⃣ **Test**  
   - Installs dependencies  
   - Runs unit and integration tests  

2️⃣ **Build & Push**  
   - Uses Docker to build and push the image to ACR  

3️⃣ **Deploy to Staging**  
   - Deploys the image from ACR to a staging slot in Azure App Service  

4️⃣ **Health Check (Staging)**  
   - Ensures the staging slot is running properly  

5️⃣ **Swap to Production**  
   - Moves the **staging** deployment to **production**  

6️⃣ **Final Health Check**  
   - Ensures the production deployment is working fine  

---

## 🔧 Prerequisites

1. **Azure App Service** with a **staging slot**  
2. **Azure Container Registry (ACR)**  
3. **Managed Identity** for Azure authentication  
4. **Azure DevOps Service Connection** for deployment  

---

## 🏆 Best Practices Used

✔ **Branch-Based Triggers**  
   - Pipeline runs only when changes are pushed to the `main` branch.

✔ **Automated Testing**  
   - Unit and integration tests run before any deployment.

✔ **Docker Layer Caching**  
   - Uses Azure DevOps Cache task to speed up Docker builds.

✔ **Azure Managed Identity**  
   - Secure authentication without storing credentials in YAML.

✔ **Zero-Downtime Deployment**  
   - Deploys to a **staging slot** before swapping to production.

✔ **Automated Health Checks**  
   - Verifies both **staging** and **production** deployments after deployment.

✔ **Rollback Mechanism**  
   - If the **staging slot** fails, production remains unaffected.

✔ **Environment Variables & Configs**  
   - Uses `APP_PORT`, `RESOURCE_GROUP`, and other variables to keep the pipeline reusable.

✔ **Fail-Fast Strategy**  
   - Each stage runs `curl -f` to verify health, failing early if needed.

✔ **Parallelization & Dependencies**  
   - Builds and deploys are structured using `dependsOn` to optimize execution.

---

## 🚀 How to Use

- Push your code to the `main` branch  
- The pipeline will **automatically** test, build, deploy, and promote the app to production  

---

## ✅ Health Check Endpoint
- Ensure your app has a `/health` endpoint that returns a `200 OK` response  

---

This pipeline ensures **zero downtime deployments** with a safe **staging-to-production** workflow. 🚀
