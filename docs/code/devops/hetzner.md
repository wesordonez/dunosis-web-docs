# Hetzner Server and Twenty CRM Set Up

!!! warning ":construction: Under Construction :construction:"

    This section is still under construction. Facts, information, and data in here may not be complete or accurate yet. 

# 🚀 Deploying Twenty CRM on a Hetzner Server with Docker & NGINX Proxy Manager

This guide walks you through deploying [Twenty CRM](https://github.com/TwentyHQ/twenty-docker) on a fresh Hetzner VPS, using Docker, NGINX Proxy Manager, and a Porkbun-registered domain.

---

## 🧱 1. Initialize Hetzner Ubuntu Server

### Connect to your server:

Can be done through SSH
```bash
ssh root@your.server.ip
```

Or through the Hetzner Server Console

### Create a new user (optional but recommended):
```bash
adduser youruser
usermod -aG sudo youruser
su - youruser
```

### Update system:
```bash
sudo apt update && sudo apt upgrade -y
```

---

## 🐳 2. Install Docker (Quick Install)

```bash
curl -fsSL https://get.docker.com | sudo sh
sudo usermod -aG docker $USER
newgrp docker  # OR log out and back in
```

---

## 🧭 3. Install Docker Compose (optional if already included)

```bash
sudo apt install docker-compose-plugin -y
```

---

## 📦 4. Deploy NGINX Proxy Manager

### Create folder and Docker Compose file:
```bash
mkdir -p ~/npm && cd ~/npm
nano docker-compose.yml
```

Paste:

```yaml
version: '3'
services:
  npm:
    image: jc21/nginx-proxy-manager:latest
    container_name: nginx-proxy-manager
    restart: always
    ports:
      - "80:80"
      - "81:81"
      - "443:443"
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

### Launch:
```bash
docker compose up -d
```

### Access Web UI:
`http://your.server.ip:81`  
_Default login: `admin@example.com` / `changeme`_

---

## 🌐 5. Point DNS to Your Server

On [Porkbun](https://porkbun.com):

| Type | Host | Answer (IP Address) | TTL |
|------|------|---------------------|-----|
| A    | crm  | your.server.ip      | 300 |

📝 This will resolve `crm.yourdomain.com` to your VPS.

---

## 📁 6. Clone and Configure Twenty CRM

### Clone the repo:
```bash
git clone https://github.com/TwentyHQ/twenty-docker.git
cd twenty-docker
```

### Create a `.env` file:
```bash
nano .env
```

Example contents:

```env
PG_DATABASE_USER=postgres
PG_DATABASE_PASSWORD=your_password
PG_DATABASE_HOST=db
PG_DATABASE_PORT=5432

NODE_PORT=3000
SERVER_URL=https://crm.yourdomain.com

REDIS_URL=redis://redis:6379

STORAGE_TYPE=local

APP_SECRET=your_random_secret
```

Generate a secure secret:
```bash
openssl rand -hex 32
```

### Add `restart: always` to `docker-compose.yml` (optional but recommended)

```yaml
restart: always
```

Apply it to each service under `services:`.

---

## 🧱 7. Start Twenty CRM

```bash
docker compose up -d
```

---

## 🔁 8. Add Domain to NGINX Proxy Manager

1. Open `http://your.server.ip:81`
2. Go to **Proxy Hosts** > **Add Proxy Host**
3. Fill in:
   - **Domain Names**: `crm.yourdomain.com`
   - **Forward Hostname / IP**: `localhost`
   - **Forward Port**: `3000`
   - ✅ Websockets Support
   - ✅ Block Common Exploits
4. Go to the **SSL** tab:
   - Enable SSL
   - Request a new Let's Encrypt certificate
   - Accept terms and enter a valid email
5. Save

---

## ✅ 9. Test It!

Visit:
```
https://crm.yourdomain.com
```

You should see the live Twenty CRM instance with a green padlock ✅

---

## 📋 10. Post-Deployment Checklist

- [ ] Ensure Docker is enabled at boot:
  ```bash
  sudo systemctl enable docker
  ```
- [ ] All containers have `restart: always`
- [ ] DNS is resolving properly
- [ ] SSL cert auto-renewal is working (NPM handles this)
- [ ] Save `.env` and secrets in a secure place

---

## 🧩 Optional Add-ons

- Add `portainer.yourdomain.com` using NPM to manage Docker visually
- Set up monitoring with Uptime Kuma or Watchtower for updates
- Configure backups for Postgres + Docker volumes

---

**Author:** Your DevOps Team @ Dunosis  
**Last updated:** {{ date }}
