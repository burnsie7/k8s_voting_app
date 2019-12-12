# k8s_voting_app

## Deploy voting app

```
kubectl create -f voting-app-pod.yaml
kubectl create -f voting-app-service.yaml
kubectl create -f redis.yaml
kubectl create -f redis-service.yaml
kubectl create -f postgres.yaml
kubectl create -f postgres-service.yaml
kubectl create -f worker-app-pod.yaml
kubectl create -f result-app-pod.yaml
kubectl create -f result-app-service.yaml
```

## Deploy Datadog

```
kubectl create -f "https://raw.githubusercontent.com/DataDog/datadog-agent/master/Dockerfiles/manifests/rbac/clusterrole.yaml"
kubectl create -f "https://raw.githubusercontent.com/DataDog/datadog-agent/master/Dockerfiles/manifests/rbac/serviceaccount.yaml"
kubectl create -f "https://raw.githubusercontent.com/DataDog/datadog-agent/master/Dockerfiles/manifests/rbac/clusterrolebinding.yaml"
kubectl create secret generic datadog-secret --from-literal api-key="<YOUR_API_KEY>"
```
