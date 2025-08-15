# Python Flask App — DevOps Example

A simple Python Flask app containerized with Docker and deployed on Kubernetes. This repo demonstrates a manual DevOps workflow (no automation/CI/CD) covering build, push, and deploy.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Prerequisites & Hardware](#prerequisites--hardware)
- [Getting Started](#getting-started)
    - [1. Clone the Code](#1-clone-the-code)
    - [2. Docker: Build, Run, and Push](#2-docker-build-run-and-push)
    - [3. Kubernetes: Deploy](#3-kubernetes-deploy)
    - [4. Updating the App](#4-updating-the-app)
    - [5. Clean Up](#5-clean-up)
- [Notes](#notes)

---

## Project Overview

**DevOps** combines software development (Dev) and IT operations (Ops) to deliver code faster and more reliably.

This project covers:
- Building a Docker image for a Flask web app
- Running and testing it locally
- Pushing to DockerHub
- Deploying manually to Kubernetes

No automation is used here; the workflow is entirely manual.

---

## Prerequisites & Hardware

- **EC2 Instance:** t2.medium (2 CPU, 4GB RAM) recommended — tested on t2.micro for Docker, then t2.medium for Kubernetes.
- **DockerHub Account** (for storing and pulling images)
- **Docker** and **kubectl** installed
- **Kubernetes Cluster** running on your EC2 instance

---

## Getting Started

### 1. Clone the Code

```bash
git clone https://github.com/bilal-amjad-dev/python-flask-app.git
cd python-flask-app
```




---

### 2. Docker: Build, Run, and Push

**a. Build the Docker Image**


```bash
docker build -t python-flask-app:v1 .
```


**b. Run the Container Locally**


```bash
docker run -it -p 5000:5000 python-flask-app:v1
```



- Open port **5000** in the EC2 security group
- Visit: `http://<EC2_PUBLIC_IP>:5000`

Press `CTRL+C` to quit the container.

**c. Push Image to DockerHub**
- Change `YOUR-DOCKERHUB-USERNAME` below to *your own* username



```bash
docker login
docker tag python-flask-app:v1 YOUR-DOCKERHUB-USERNAME/python-flask-app:v1
docker push YOUR-DOCKERHUB-USERNAME/python-flask-app:v1
```


Be sure to change your DockerHub username wherever needed.

---

### 3. Kubernetes: Deploy

1. **Edit** `k8s/manifests/deployment.yaml`
    - Change:
      ```
      image: YOUR-DOCKERHUB-USERNAME/python-flask-app:v1
      ```
      to use your DockerHub username.

2. **Deploy:**



```bash
kubectl apply -f k8s/manifests/deployment.yaml
kubectl apply -f k8s/manifests/service.yaml
```




- Open port **32402** in the EC2 security group
- Visit: `http://<EC2_PUBLIC_IP>:32402`

---

### 4. Updating the App

To update your app (for example, change response in `app.py` to `"Well done!"`):

**a. Build and push new version**



```bash
docker build -t python-flask-app:v2 .
docker tag python-flask-app:v2 YOUR-DOCKERHUB-USERNAME/python-flask-app:v2
docker push YOUR-DOCKERHUB-USERNAME/python-flask-app:v2
```




**b. Update Kubernetes deployment**
- Change the image tag in `deployment.yaml`:


```bash
image: YOUR-DOCKERHUB-USERNAME/python-flask-app:v2
```


- Reapply deployment:


```bash
kubectl apply -f k8s/manifests/deployment.yaml
```



---

### 5. Clean Up

After finishing:



```bash
kubectl delete -f k8s/manifests/deployment.yaml
kubectl delete -f k8s/manifests/service.yaml
```




---

## Notes

- **Manual Steps:** This project uses *manual* build and deployment (no CI/CD).
- **Security Groups:** Always open the appropriate port for Docker or Kubernetes access.
- **Customization:** Update your DockerHub username anywhere it appears.
- For automation, look into CI/CD tools like GitHub Actions and Helm for future improvements.

---





**What is Devops?**

In devops, we have code.

the code is:
- build (Dockerfile, Image, run_container_locally, Push),
- and Deploy (Kubernetes).

When a developer makes a commit in code, the code is:
- build (Dockerfile, Image, run_container_locally, Push),
- and Deploy (Kubernetes).

In this project, we achieve this manual means without automation. 

To do this project, we need t2.medium. Means 2 cpu and 4 gb ram.  

I practiced this using t2.micro when i was practicng docker. Afterthat, I practiced on t2.medium. 

To this project, you need to change:
- Your dockerhub username in docker tag and docker push command
- Your dockerhub username in deployment.yaml file 





## Code (GitHub)
```bash
git clone https://github.com/bilal-amjad-dev/python-flask-app.git
```
```baash
cd python-flask-app
```



## Build (Docker) 
(Dockerfile, Image, Container, Push)
- **Image**
```bash
docker build -t python-flask-app:v1 .
```

- **Container**
```bash
docker run -it -p 5000:5000 python-flask-app:v1
```

Note, please open port 5000 of your security group.

Access the app at: http://<EC2_PUBLIC_IP>:5000.



Press CTRL+C to quit


- **Push**
Please change your dockerhub username in `docker tag` and `docker push` commands.

```bash
docker login
```
```bash
docker tag python-flask-app:v1 YOUR-DOCKERHUB-USERNAME/python-flask-app:v1
```
```bash
docker push YOUR-DOCKERHUB-USERNAME/python-flask-app:v1
```

Please write here your dockerhub username. 

## Deploy (Kubernetes)

Please change your dockerhub username in `deployment.yaml` file. 
```bash
image: YOUR-DOCKERHUB-USERNAME/python-flask-app:v1  # 👈 Please write here your own dockerhub username
```

```bash
kubectl apply -f k8s/manifests/deployment.yaml
kubectl apply -f k8s/manifests/service.yaml
```

Please open port 32402 of your security group. (Mentioned in service.yaml)

Access the app at: http://<EC2_PUBLIC_IP>:32402.




Everything is working fine. 

### Make a commit, Update the App (v2)


Modify app.py to return "Well done!".




So, according to your DovOps circle, it is:
- Code
- Build (Dockerfile, Image, locally_run_container, Push)
- Deploy
We have to build the image and then push.

```bash
docker build -t python-flask-app:v2 .
docker tag python-flask-app:v2 YOUR-DOCKERHUB-USERNAME/python-flask-app:v2
docker push YOUR-DOCKERHUB-USERNAME/python-flask-app:v2
```


### Update deployment.yaml to use v2 and reapply:

```bash
image: YOUR-DOCKERHUB-USERNAME/python-flask-app:v1  # 👈 Please write here your own dockerhub username and write v2
```


```bash
kubectl apply -f deployment.yaml
```


After lab, please delete resources:



