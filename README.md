# Getting Started with K3D

Run a Kubernetes cluster locally with Docker.

## Create cluster

Create a cluster binding the port 8000 of your computer to port 30000 of the cluster with 3 nodes (master and 2 agents)

```
k3d cluster create -p "8000:30000@loadbalancer" --agents 2
```

Set the cluster context on kubectl

```
$kubectl config use-context k3d-k3s-default

Switched to context "k3d-k3s-default"
```

View cluster info

```
$ kubectl cluster-info

Kubernetes master is running at https://0.0.0.0:35879
CoreDNS is running at https://0.0.0.0:35879/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://0.0.0.0:35879/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy
```
## Create pod for application

The file deployment.yaml contains a simple deployment for a nginx container exposing the port 80

```
kubectl apply -f deployment.yaml
```

## Create service to access the application

The file service.yaml expose a NodePort to bind 8000 -> 30000 -> 80

```
kubectl apply -f service.yaml
```

## Delete cluster

```
k3d cluster delete
```