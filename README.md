# Nexus Flow Engine (AppFlowy Self-Hosted)

A robust, self-hosted deployment configuration for AppFlowy, optimized for containerized environments like **Dokploy** (Docker Swarm/Compose).

## 🚀 Features

*   **Full Stack**: Contains all necessary microservices (Cloud, Web, Auth, Database, Storage).
*   **Production Ready**: Configured with Nginx as an internal gateway and Traefik labels for Dokploy.
*   **Secure Auth**: Pre-configured for GoTrue with SMTP (Email) and OAuth support.

## 🛠 Deployment Guide (Dokploy)

This repository is designed to be deployed directly via Dokploy's **GitHub** integration.

### 1. Prerequisites
*   A Dokploy server set up.
*   A domain or sub-domain (e.g., `flowy.yourdomain.com`) pointing to your server IP via Cloudflare (Proxy OFF initially).
*   An SMTP provider for emails (Gmail, SendGrid, SES, etc.).

### 2. Connect Repository
1.  In Dokploy, go to your Project.
2.  Click **Create Service** -> **Compose**.
3.  Choose **GitHub** as the provider (Ensure your GitHub account is connected in Dokploy settings).
4.  Select this repository: `SE2-Coder/nexus-flow-engine`.
5.  Branch: `main`.

### 3. Environment Configuration
1.  Go to the **Environment** tab in your new service.
2.  Copy the contents of `.env.example`.
3.  **IMPORTANT**: Fill in the real values:
    *   **Domain**: Replace `your-domain.com` with your actual domain in all URLs (`APPFLOWY_BASE_URL`, `APPFLOWY_WEB_URL`, etc).
    *   **Secrets**: Generate strong passwords for `POSTGRES_PASSWORD`, `AWS_SECRET`, and `GOTRUE_JWT_SECRET`.
    *   **Email**: Fill in the `SMTP` section. Without this, you cannot register users.

### 4. Deploy & Expose
1.  Click **Deploy**.
2.  Once running (Green status), go to the **Domains** tab.
3.  Add your domain:
    *   **Service**: `nginx`
    *   **Port**: `80`
    *   **Path**: `/`
    *   **HTTPS**: Enable Let's Encrypt.
4.  Click **Create**.

## 📧 Email Setup (SMTP)

To enable user registration, you need an SMTP server.

**Example (Gmail):**
*   Host: `smtp.gmail.com`
*   Port: `465`
*   User: `your@gmail.com`
*   Pass: `your-app-password` (Not your login password, generate one in Google Account Security).

## 🔒 OAuth Setup (Optional)

To enable "Login with Google/GitHub":
1.  Create an OAuth App in the provider's developer console.
2.  Set the Callback URL to: `https://your-domain.com/gotrue/callback`.
3.  Add the Client ID and Secret to your Dokploy Environment variables.
