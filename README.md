# Updapt - Automated CI/CD to Azure

**Architecture**: GitHub Actions builds Docker images → pushes to Docker Hub → SSH deploys to Azure Windows VM with health check + auto-rollback.

**Live**: `http://135.13.9.205/health` 

**Tech**: React + Node.js + Nginx + Docker Compose + GitHub Actions

**Pipeline**: 
1. Push to `main` triggers build
2. Images tagged `latest` + `<git-sha>` pushed to Docker Hub
3. SSH to VM → `git pull` → `docker compose pull` → `docker compose up -d`
4. Health check `/health` - rollback if not 200

**Verify deployment**:
```powershell
docker ps
curl.exe -s http://localhost/health

notepad C:\ProgramData\ssh\sshd_config


# Logging
SyslogFacility AUTH
LogLevel INFO

StrictModes no
PubkeyAuthentication yes

