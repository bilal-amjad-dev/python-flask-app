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



