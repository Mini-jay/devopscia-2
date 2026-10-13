## Kubernetes Deployment

### Resources

- `deployment.yaml` defines an NGINX Deployment using image `nginx:1.27` with two initial replicas.
- `service.yaml` exposes the Deployment using a NodePort Service on port `30080`.

### Deploy

Run these commands from the repository root:

```powershell
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### Verify the deployment

```powershell
kubectl get nodes
kubectl get deployments
kubectl get pods
kubectl get services
```

The Deployment should initially have two ready replicas.

### Access NGINX

```powershell
minikube service nginx-service
```

This command opens the service in a browser or prints a URL to access it.

### Scale to three replicas

```powershell
kubectl scale deployment nginx-deployment --replicas=3
kubectl get deployments
kubectl get pods
```

Verify that all three replicas become ready.

### Verify self-healing


```powershell
kubectl delete pod <pod-name>
kubectl get pods
```

Kubernetes should create a replacement pod so that the Deployment returns to three replicas.

