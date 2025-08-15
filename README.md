

To this project, you need to change:
- Your dockerhub username in docker push command
- Your dockerhub username in deployment.yaml file 





## Code (GitHub)
```bash
git clone https://github.com/bilal-amjad-dev/python-flask-app.git
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
docker run -it -p 5000:5000 python-flask-app:v1:v1
```

- **Push**
```bash
docker login
docker tag python-flask-app:v1 YOUR-DOCKERHUB-USERNAME/python-flask-app:v1
docker push YOUR-DOCKERHUB-USERNAME/python-flask-app:v1
```


## Deploy (Kubernetes)


```bash
kubectl apply -f k8s/manifests/deployment.yaml
kubectl apply -f k8s/manifests/service.yaml
```






