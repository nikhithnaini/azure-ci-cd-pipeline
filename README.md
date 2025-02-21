# azure-ci-cd-pipeline
# Node.js CI/CD Pipeline

This pipeline deploys a Node.js/TypeScript app to Azure App Service using Azure DevOps, Docker, and Azure Container Registry (ACR).

## Pipeline Stages
- **Test**: Runs tests on source code.
- **BuildAndPush**: Builds and pushes Docker image to ACR.
- **Deploy**: Deploys to Azure App Service.
- **HealthCheck**: Verifies the app is running.

## Why This Setup?

1. **Self-Hosted Agent (Optional)**:
   - Why: Could use a VM for control and caching, but uses `ubuntu-latest` for simplicity.

2. **Managed Identity**:
   - Why: Secures ACR and App Service access without credentials via `az login --identity`.

3. **Using `az acr` Instead of Docker**:
   - Why: Integrates with ACR using Managed Identity, keeping it Azure-native.

4. **Optional Cache Step**:
   - Why: Caches Docker layers to speed builds, optional since code changes are infrequent.

## Notes
- Tests run before build to fail fast.
- Assumes a `/health` endpoint—adjust if needed.
- Update Node.js version (16.x) to match your app.

## Prerequisites
- Azure DevOps, ACR, and App Service setup.
- Managed Identity with `AcrPush` and `Contributor` roles.
- `Dockerfile` in the repo root.
