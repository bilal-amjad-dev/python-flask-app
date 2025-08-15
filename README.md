To do this project, we need t2.medium. 

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
kubectl apply -f k8s/manifests/deployment.yaml
kubectl apply -f k8s/manifests/service.yaml
```






