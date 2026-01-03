# Secure CI/CD Pipeline

A production-ready CI/CD pipeline for Node.js applications, featuring automated security scanning, Docker containerization, and seamless deployment to AWS App Runner.

##  Technologies

-   **Runtime**: Node.js, Express
-   **CI/CD**: GitHub Actions
-   **Security**: Semgrep (SAST), npm audit (SCA), Gitleaks (Secret Scanning)
-   **Containerization**: Docker
-   **Registry**: AWS Elastic Container Registry (ECR)
-   **Deployment**: AWS App Runner

---

##  Setup Instructions

Follow these steps to set up the pipeline for your own AWS account.

### 1. AWS Configuration

#### A. Create an IAM User
1.  Log in to the **AWS Console**.
2.  Go to **IAM** -> **Users** -> **Create user**.
3.  Name it `github-actions-user`.
4.  Attach policies directly:
    -   `AmazonEC2ContainerRegistryFullAccess`
    -   `AWSAppRunnerFullAccess`
5.  Create **Access Keys** for this user and save the `Access Key ID` and `Secret Access Key`.

#### B. Create ECR Repository
1.  Go to **Amazon ECR**.
2.  Click **Create repository**.
3.  Name it: `secure-ci-cd`.
4.  Keep other settings as default and click **Create**.

### 2. GitHub Secrets Configuration

To allow GitHub Actions to interact with your AWS account, you need to add secrets.

1.  Go to your GitHub Repository.
2.  Navigate to **Settings** -> **Secrets and variables** -> **Actions**.
3.  Click **New repository secret** and add the following:

| Secret Name | Value Description | Example |
| :--- | :--- | :--- |
| `AWS_ACCESS_KEY_ID` | The Access Key ID from Step 1A | `AKIA...` |
| `AWS_SECRET_ACCESS_KEY` | The Secret Access Key from Step 1A | `wJalr...` |
| `AWS_REGION` | Your preferred AWS Region | `us-east-1` |

### 3. App Runner Setup (One-Time)

Once your secrets are added and you push code to `main`, the pipeline will build and push the image to ECR. Now, link it to App Runner:

1.  Go to **AWS App Runner Console**.
2.  Click **Create Service**.
3.  **Source**: Select **Container Registry** -> **Amazon ECR**.
4.  **Image URI**: Browse and select the `secure-ci-cd` image (tag: `latest`).
5.  **Deployment Settings**: Select **Automatic** (Trigger: New push to ECR).
6.  **Configuration**:
    -   **Port**: `3000`
7.  **Create & Deploy**.

Once deployed, App Runner provides a **Default Domain**. Your pipeline will now display this URL in the logs!

---

## 💻 Local Development

To run the application locally:

```bash
# Navigate to the app directory
cd app

# Install dependencies
npm install

# Start the server
npm start
```

Visit `http://localhost:3000` to see the application.
