# k8s_voting_app

## If running in GKE

```
kubectl create clusterrolebinding cluster-admin-binding --clusterrole cluster-admin --user $(gcloud config get-value account)
```

## Create secrets for agent(s)

```
kubectl create secret generic datadog-api --from-literal=token=___INSERT_API_KEY_HERE___
kubectl create secret generic datadog-app --from-literal=token=___INSERT_APP_KEY_HERE___
kubectl create secret generic datadog-auth-token --from-literal=token=12345678901234567890123456789012
```

## Kube state metrics (optional)

```
kubectl create -f kube-state-metrics
```

## Create RBAC Permissions

```
kubectl create -f "https://raw.githubusercontent.com/DataDog/datadog-agent/master/Dockerfiles/manifests/rbac/clusterrole.yaml"
kubectl create -f "https://raw.githubusercontent.com/DataDog/datadog-agent/master/Dockerfiles/manifests/rbac/serviceaccount.yaml"
kubectl create -f "https://raw.githubusercontent.com/DataDog/datadog-agent/master/Dockerfiles/manifests/rbac/clusterrolebinding.yaml"
```

## Deploy Datadog Agent(s)

```
kubectl apply -f datadog-agent/datadog-cluster-agent.yaml
kubectl create -f datadog-agent/datadog-agent.yaml
```

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

## copy/paste for testing

```
kubectl delete daemonset datadog-agent
kubectl delete deployment datadog-cluster-agent
kubectl apply -f datadog-agent/datadog-cluster-agent.yaml
kubectl create -f datadog-agent/datadog-agent.yaml
```
