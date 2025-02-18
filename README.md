<h1 align="center">
  <br>
  <a href=""><img src="/img/logo.png" alt="" width="300px;"></a>
  <br>
  <img src="https://img.shields.io/badge/PRs-welcome-blue">
  <img src="https://img.shields.io/github/last-commit/kh4sh3i/DefectDojo">
  <img src="https://img.shields.io/github/commit-activity/m/kh4sh3i/DefectDojo">
  <a href="https://twitter.com/intent/follow?screen_name=kh4sh3i_"><img src="https://img.shields.io/twitter/follow/kh4sh3i_?style=flat&logo=twitter"></a>
  <a href="https://github.com/kh4sh3i"><img src="https://img.shields.io/github/stars/kh4sh3i?style=flat&logo=github"></a>
</h1>


# DefectDojo
DefectDojo is a DevSecOps, ASPM (application security posture management), and vulnerability management tool. 


DefectDojo can be installed using several methods, including Docker Compose, Kubernetes, SaaS, or package installation. Below are the steps for the most common installation methods:


# 1. Docker Compose Installation (Recommended)
* Docker version 19.03.0+ and Docker Compose 1.28.0+.
* A system with at least 2 vCPUs, 8GB RAM, and 2GB disk space.

```
# Clone the project
git clone https://github.com/DefectDojo/django-DefectDojo
cd django-DefectDojo

# Check if your installed toolkit is compatible
./docker/docker-compose-check.sh

# Building Docker images
docker compose build

# Run the application (for other profiles besides postgres-redis see  
# https://github.com/DefectDojo/django-DefectDojo/blob/dev/readme-docs/DOCKER.md)
docker compose up -d

# Obtain admin credentials. The initializer can take up to 3 minutes to run.
# Use docker compose logs -f initializer to track its progress.
docker compose logs initializer | grep "Admin password:"
```

# 2. Offline Installation
```
# in internet system download repo :
git clone https://github.com/DefectDojo/django-DefectDojo.git
cd django-DefectDojo
docker compose build


# Save Docker Images:
docker save -o defectdojo.tar defectdojo/defectdojo-django
docker save -o nginx.tar defectdojo/defectdojo-nginx
docker save -o postgres.tar postgres
docker save -o redis.tar redis

# Step 2: Install on the Offline Machine
docker load -i defectdojo.tar
docker load -i nginx.tar
docker load -i postgres.tar
docker load -i redis.tar

# Access DefectDojo:
http://localhost:8080/
```


## Tips
* if you install defectdojo in windows it is better to install (docker desktop + WSL v2)
* if you install defectdojo in vmware system it is better use (docker decktop + hyper-v) 
* we get error wsl.exe --update in offline mode in windows in vmware we should use hyper-v instead

