# Secure CI/CD

CI/CD pipeline with security scanning for Node.js application. GitHub Actions workflow runs Semgrep, npm audit, and Gitleaks on every push.

## Technologies

Node.js • Express • GitHub Actions • Semgrep • npm audit • Gitleaks • Docker • AWS ECR • AWS App Runner

## Deployment Setup (One-Time)

To enable the live application URL in your pipeline, follow these steps once:

1.  **Push the Code**: Ensure your latest code is pushed to GitHub so the image is built and pushed to ECR.
2.  **Go to AWS App Runner**: Open the [AWS App Runner Console](https://console.aws.amazon.com/apprunner).
3.  **Create Service**:
    *   Click **Create Service**.
    *   **Source**: Select **Container Registry** -> **Amazon ECR**.
    *   **Image URI**: Browse and select your `secure-ci-cd` image (tagged `latest`).
    *   **Deployment settings**: Choose **Automatic** (this enables auto-deploy on new pushes).
    *   **Roles**: Create/Select a service role that has permission to pull from ECR.
4.  **Configure Service**:
    *   **Service Name**: `secure-ci-cd-service` (or similar).
    *   **Port**: `3000`.
5.  **Create & Deploy**: Click create.
6.  **Get the URL**: Once deployed, copy the "Default domain" URL.

Your pipeline is now fully automated! 🚀