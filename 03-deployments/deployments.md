# Deployment

## Apply

### Create or update the deployment from YAML

```sh
kubectl apply -f nginx-deployment.yaml
```

### List deployments in the namespace
```sh
kubectl get deployments -n staging
```

### Detailed status: looking at 'Conditions' and 'Events'
```sh
kubectl describe deployment nginx-demo -n staging
```

### Watch pods come up live during a rollout
```sh
kubectl get pods -n staging -l app=nginx-demo -w
```

## Update and rollback

### Bump nginx version: triggers a rolling update immediately
```sh
kubectl set image deployment/nginx-demo   nginx=nginx:1.27-alpine   -n staging
```

### Check rollout progress
```sh
kubectl rollout status deployment/nginx-demo -n staging
```

### See rollout history: each apply with a change quals a new revision)
```sh
kubectl rollout history deployment/nginx-demo -n staging
```

### Roll back to previous version
```sh
kubectl rollout undo deployment/nginx-demo -n staging
```

### Roll back to a specific revision
```sh
kubectl rollout undo deployment/nginx-demo   --to-revision=3 -n staging
```

## Scale and verify

### Manually scale up
```sh
kubectl scale deployment nginx-demo --replicas=6 -n staging
```

### Quick smoke test — port-forward to your local machine
```sh
kubectl port-forward deployment/nginx-demo 8080:80 -n staging

# open http://localhost:8080 and you'll see nginx's welcome page
```

### Check HPA if autoscaling is configured
```sh
kubectl get hpa -n staging
```
