- The ML model is deployed with the ingress kubernetes feature.
- Ingress exposes the apps to outside world.
- Kubernetes Ingress is a local kubernetes resource for routing traffic from an external source to service endpoints in the cluster.

### 0. Pip Install Requirements

```
pip install -r requirements.txt
```

### 1. Build container

```
docker image build -t ml_kubectl_ingress .
```

### 2. Run container

```
docker run --rm --name ml_kubectl_ingress -p 8002:8000 -d ml_kubectl_ingress
```

### 3. Cauntion IP

- First do step 4 if you get this error "ErrImageNeverPull" follow below steps

```
kubectl describe pod id
```

* If you have linux, you have to alter or add some code.

```
sudo vim etc/host
```
- Add cluster ip and host address name

- Check 

```
kubectl get svc
```

```
ping host_address_name
```

* If you have windows, you have to alter or add some code.

```
C:\Windows\System32\Drivers\etc\hosts
```
- Run in administrator mode

- Add IP and host name



### 4. Build 

```
kubectl apply -f ml-prediction-deployment.yaml
```

```
kubectl get pods -w
```


### 5. Create service

```
kubectl create service nodeport ml-prediction --tcp=8000:8000
```

```
kubectl get services
```

### 6. Ingress

```
minikube addons enable ingress
```

```
kubectl apply -f ingress-ml-prediction.yaml
```

```
kubectl get ingress
```

### 7. Delete

```
kubectl delete -f ml-prediction-deployment.yaml
```

```
kubectl get all
```

```
kubectl delete service/ml-prediction
```

```
kubectl get service
``` 