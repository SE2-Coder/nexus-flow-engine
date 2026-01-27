# Nexus Flow Engine (AppFlowy Self-Hosted)

A robust, self-hosted deployment configuration for AppFlowy, optimized for containerized environments like Dokploy (Docker Swarm/Compose).

## 🚀 Features

*   **Full Stack**: Includes AppFlowy Cloud, Web, Admin Frontend, Worker, GoTrue (Auth), Postgres, Redis, and MinIO.
*   **Reverse Proxy**: Pre-configured Nginx gateway to route traffic to internal microservices.
*   **Production Ready**: Optimized `docker-compose.yml` with health checks, restart policies, and volume persistence.
*   **Dokploy Compatible**: Ready to be deployed as a Docker Compose Stack.

## 🛠 Deployment Guide (Dokploy)

1.  **Clone/Connect**: Connect this repository to your Dokploy project.
2.  **Environment Variables**: Copy the content of `.env.example` to the **Environment** tab in Dokploy.
    *   Update `APPFLOWY_BASE_URL`, `APPFLOWY_WEB_URL`, and `API_EXTERNAL_URL` to your actual domain (e.g., `https://flowy.yourdomain.com`).
    *   Update `APPFLOWY_WS_BASE_URL` to `wss://flowy.yourdomain.com/ws/v2`.
    *   Set secure passwords for Postgres and MinIO.
3.  **Deploy**: Click "Deploy".
4.  **Domain Mapping**: In Dokploy, point your domain to the `nginx` service (Port 80).

## 📂 Architecture

*   **Nginx**: Entry point (Port 80/443).
*   **AppFlowy Cloud**: Core API (Port 8000).
*   **AppFlowy Web**: Frontend (Port 80).
*   **GoTrue**: Authentication Service (Port 9999).
*   **Postgres**: Database (Port 5432).
*   **Redis**: Cache & Message Broker.
*   **MinIO**: S3-compatible Object Storage.
