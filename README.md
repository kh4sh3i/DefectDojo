<h1 align="center">
  <br>
  <img src="/img/logo.png" alt="" width="300px;">
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


## 1. Docker Compose Installation (Recommended)
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

## 2. Offline Installation
```
# in internet system download repo :
git clone https://github.com/DefectDojo/django-DefectDojo.git
cd django-DefectDojo
docker compose build



# add tags to postgres & redis, because this image dos not any tag!
docker images
docker tag <postgres_image_id> postgres:latest
docker tag <redis_image_id> redis:latest



# Save Docker Images:
docker save -o defectdojo.tar defectdojo/defectdojo-django
docker save -o nginx.tar defectdojo/defectdojo-nginx
docker save -o postgres.tar postgres
docker save -o redis.tar redis


# Install on the Offline Machine
docker load -i defectdojo.tar
docker load -i nginx.tar
docker load -i postgres.tar
docker load -i redis.tar
```
### edit docker-compose in offline machine
```
notepad docker-compose.yml

.
.
.
version: '3'
services:
  defectdojo:
    image: defectdojo/defectdojo-django:latest  # Ensure this matches your local image name
    ports:
      - "8080:8080"
...

# we should change redis and postgres to new local address :
image: postgres:latest 
image: redis:latest 

```


```
# create container and run app
docker compose up -d


# find password for user: admin
docker compose logs initializer | find "Admin password:"


# Access DefectDojo:
http://localhost:8080/
```

<h1 align="center">
  <img src="./img/docker.png" width="100%;">
</h1>

### asvs
we can use defectdojo benchmark for checking ASVS
<h1 align="center">
  <img src="./img/asvs.png" width="100%;">
</h1>




### demo 
```
https://demo.defectdojo.org/dashboard
admin
1Defectdojo@demo#appsec
```


## Tips
* if you install defectdojo in windows it is better to install (docker desktop + WSL v2)
* if you install defectdojo in vmware system it is better use (docker decktop + hyper-v) 
* we get error wsl.exe --update in offline mode in windows in vmware we should use hyper-v instead
* we use "find" instead of "grep" in windows
* we use "notepad" instead of "vim" for editing file in windows
* redis & postgres dose not ant tags and after export with and "load" in new machine not detect and docker compose try to download this image from the net ! we should add tags for prevent this issue


### refrences
* [defectdojo](https://github.com/DefectDojo/django-DefectDojo)