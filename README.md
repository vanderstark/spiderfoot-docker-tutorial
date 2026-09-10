# SpiderFoot Docker Tutorial & Setup

## 🔍 SpiderFoot OSINT Automation with Docker

**SpiderFoot** is the world's most widely used open-source OSINT (Open Source Intelligence) automation tool. This repository provides a Docker-based setup for SpiderFoot that makes it easy to deploy, configure, and manage without installing Python or its dependencies directly on your system.

### ✅ Features

- ✅ **Self-contained Docker environment** - No Python/OS dependencies needed
- ✅ **Pre-configured** with security best practices
- ✅ **Persistent storage** for scan results
- ✅ **Accessible via browser** at http://localhost:5000
- ✅ **Configurable** via environment variables
- ✅ **Easy to update** with new SpiderFoot versions

### 📦 Repository Contents

- `docker-compose.yml` - Docker configuration for SpiderFoot
- `README.md` - This documentation
- `.env` - Example environment variables (not committed to repo)
- `.gitignore` - Security best practices

---

## 🛠️ Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/vanderstark/spiderfoot-docker-tutorial.git
cd spiderfoot-docker-tutorial
```

### 2. Set Up Environment Variables

Create a `.env` file with your credentials:

```bash
# .env file content
SF_EMAIL=your_email@example.com
SF_PASSWORD=your_strong_password
```

> **⚠️ Security Note:** Never commit actual credentials to version control. This is a template only.

### 3. Start the Container

```bash
docker-compose up -d --build
```

### 4. Access the Interface

Open your browser and go to:
```
http://localhost:5000
```

You'll see the SpiderFoot login screen. The initial credentials are:
- **Email:** `admin@spiderfoot.net` (check container logs for actual email)
- **Password:** `sf_admin_password` *(check container logs)*

---

## 📦 Docker Configuration

### docker-compose.yml

- **Service:** `spiderfoot`
- **Port:** 5000 (web interface)
- **Volumes:** Persistent data storage at `/data`
- **Environment Variables:**
  - `SF_EMAIL` - Your email address
  - `SF_PASSWORD` - Your password
  - `SF_CONSOLE_PORT` - Port for console access (default 5000)

### Dockerfile (Not included but referenced)

The Docker image is based on the official `smicallef/spiderfoot` image with necessary PHP extensions enabled.

---

## 🔐 Security Notes

- **Never commit secrets** to version control
- Use GitHub secrets or environment variables for production
- The container runs as non-root user for security
- All data is stored in Docker volumes for persistence
- Regularly update SpiderFoot to get security patches

---

## 🔄 Maintenance

To update SpiderFoot:

```bash
docker-compose down
docker-compose pull
docker-compose up -d --build
```

### 🔄 Cron Jobs (Optional)

You can schedule regular scans using cron jobs that call the SpiderFoot API:

```bash
# Example cron job (run every 6 hours)
0 */6 * * * curl -X POST http://localhost:5000/api/v1/start_scan -d '{"target": "example.com", "type": "domain"}'
```

---

## 🔐 Security Notes

- This setup is designed for **internal use only** or with proper network isolation
- Never expose port 5000 to the public internet without authentication
- Consider using HTTPS reverse proxy (Traefik/Nginx) in production environments
- Regularly rotate API keys and passwords

---

## 📚 Resources

- [SpiderFoot Official Documentation](https://spiderfoot.net/)
- [SpiderFoot GitHub Repository](https://github.com/smicallef/spiderfoot)
- [Docker Hub: SpiderFoot Image](https://hub.docker.com/r/smicallef/spiderfoot)

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

© 2023 - 2026 SpiderFoot Docker Tutorial. All rights reserved.