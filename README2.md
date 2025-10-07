# Hello World App on Minikube

A simple Flask app deployed to a local Minikube cluster via helm. Argocd implementation ensures whenever there is a change in the helm chart then the application is updated

---
## Steps to Run

### 1. Start Minikube

Make sure you have Minikube installed. Then, start a local Minikube cluster:
```bash
minikube start
```

### 2. Set Minikube to use docker daemon

```bash
eval $(minikube docker-env)
```

### 3. Build Docker img and push - make sure img tag matches in the values.yaml file
```
cd app/
docker build -t ioioioioio/hello-world:latest .
docker push ioioioioio/hello-world
```

### 4. Navigate to helm directory and install the chart
```
helm install hello-world .  
```

### 5. Access app
```
minikube service hello-world
```

### 6. If you make changes to the code, you need to redeploy by running
```
docker build -t ioioioioio/hello-world:latest .
docker push ioioioioio/hello-world
```

### Brief description on how to install argocd on minikube
```
1. kubectl create ns argocd
2. kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.5.8/manifests/install.yaml
3. kubectl get all -n argocd
4. kubectl port-forward svc/argocd-server -n argocd 8080:443
5. access via localhost:8080
6. get login password by running kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo - username is admin
```

## Multiple environments
Argocd can create an application for each environment and this would require a helm chart directory with values files for each env. The same chart is used but the values.yaml is different. 