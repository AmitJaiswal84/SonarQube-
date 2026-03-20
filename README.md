🚀 SonarQube Production Setup (Docker + PostgreSQL)

This repository provides a production-ready Docker Compose setup for deploying SonarQube LTS (Community Edition) with a PostgreSQL database.

It is designed for:

Stable deployments

Persistent storage

CI/CD integration

Scalability (can be extended with reverse proxy & external DB)

📌 Architecture Overview

SonarQube → Code quality analysis platform

PostgreSQL → Backend database

Docker Compose → Container orchestration

📦 Tech Stack

SonarQube LTS Community

PostgreSQL 15

Docker & Docker Compose

⚙️ Prerequisites
Minimum Requirements (Production Recommended)
Resource	Minimum	Recommended
CPU	2 Core	4 Core
RAM	4 GB	8 GB+
Disk	10 GB	50 GB SSD
Software Requirements

Docker ≥ 20.x

Docker Compose ≥ 1.29 / v2

Linux-based system (Recommended: Ubuntu / RHEL)

📂 Repository Structure
.
├── docker-compose.yml
├── README.md
🔐 Configuration
Environment Variables

Configured inside docker-compose.yml:

Variable	Description
SONAR_JDBC_URL	PostgreSQL connection URL
SONAR_JDBC_USERNAME	DB username
SONAR_JDBC_PASSWORD	DB password

👉 Important: Change default credentials before production use.

▶️ Deployment Steps
1️⃣ Clone Repository
git clone <your-repo-url>
cd <repo-folder>
2️⃣ Update System Limits (Mandatory)
sysctl -w vm.max_map_count=262144
sysctl -w fs.file-max=65536
ulimit -n 65536

Make it permanent:

echo "vm.max_map_count=262144" >> /etc/sysctl.conf
echo "fs.file-max=65536" >> /etc/sysctl.conf
sysctl -p
3️⃣ Start Services
docker-compose up -d
4️⃣ Verify Deployment
docker ps

Check logs if needed:

docker logs sonarqube
docker logs sonarqube-db
🌐 Access Application

URL: http://<server-ip>:9000

Default Credentials
Username: admin
Password: admin

⚠️ You must change the password after first login.

💾 Data Persistence

Docker volumes ensure persistent storage:

Volume	Purpose
sonarqube_data	Application data
sonarqube_extensions	Plugins
sonarqube_logs	Logs
postgres_data	Database
🔒 Production Best Practices
1. Change Default Credentials

Update DB username/password

Change SonarQube admin password

2. Use External Database (Recommended)

For production, consider:

AWS RDS PostgreSQL

Managed DB for better backup & HA

3. Enable Reverse Proxy (Nginx)

Add SSL (HTTPS)

Configure domain (e.g., sonar.company.com)

4. Backup Strategy

Schedule PostgreSQL backups

Backup Docker volumes regularly

5. Resource Monitoring

Monitor CPU / Memory usage

Integrate with:

Prometheus

Grafana

🔧 Scaling & Improvements

Move PostgreSQL to managed service

Deploy SonarQube on Kubernetes

Add CI/CD integration:

Bitbucket Pipelines

Jenkins

GitHub Actions

⚠️ Known Limitations

Community Edition does not support:

High Availability (HA)

Multi-node clustering

Suitable for small to medium teams

🛠 Troubleshooting
SonarQube not starting
docker logs sonarqube
Database issues
docker logs sonarqube-db
Port conflict

Update port mapping:

ports:
  - "9001:9000"
📈 Future Enhancements

SSL automation with Let's Encrypt

AWS deployment (EC2 + RDS + ALB)

Automated backups using cron

Integration with DevSecOps pipeline

🏁 Summary

This setup provides a robust, scalable, and production-ready foundation for running SonarQube using Docker.

If you want next step, I can help you:
👉 Add Nginx + SSL setup
