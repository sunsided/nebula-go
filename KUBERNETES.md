# Nebula Graph Kubernetes Deployment

Please find the information in [How to Deploy Nebula Graph on Kubernetes](https://nebula-graph.io/posts/how-to-deploy-nebula-graph-in-kubernetes/).

The Helm chart is taken from the official repository [vesoft-inc/nebula/kubernetes/helm](https://github.com/vesoft-inc/nebula/tree/master/kubernetes/helm).

## Deploy

### Cluster Topology

The following is a hypothetical cluster topology for just running
Nebula Graph without any UIs such as Graph Studio:

| Server IP   | Nebula Services             | Role       |
|-------------|-----------------------------|------------|
| x.x.x.x     |                             | k8s-master |
| x.x.x.x     | graphd, metad-0, storaged-0 | k8s-slave  |
| x.x.x.x     | graphd, metad-1, storaged-1 | k8s-slave  |
| x.x.x.x     | graphd, metad-2, storaged-2 | k8s-slave  |

## Local Development using Kind

### Setting up a cluster for Nebula

Install kind as described [here](https://kind.sigs.k8s.io/docs/user/quick-start/), then create
a new Kubernetes cluster called `nebula` like so:

```
kind create cluster --name nebula --config=kind/config.yaml
```

You should be presented with output similar to the following:

```
Creating cluster "nebula" ...
 ✓ Ensuring node image (kindest/node:v1.20.2) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-nebula"
You can now use your cluster with:

kubectl cluster-info --context kind-nebula

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
```

### Switching to the cluster

```bash
kubectl cluster-info --context kind-nebula
kubectl config use-context kind-nebula
```

### Installing the Helm chart

Make sure to select the correct Kubernetes context by either using `kubectl config use-context kind-nebula` or by specifying the `--kube-context=kind-nebula` to Helm.


```bash
kubectl config use-context kind-nebula

# helm install nebula helm/ # WARNING! You'll need to add options to apply your configuration!
helm install nebula helm/ --set=storage.storageClass=standard --set=nodeSelector=null --dry-run

helm list
```

This will spin up the appropriate pods using the default configuration.

### Port-forwarding

Accessing Nebula through the client:

```bash
kubectl port-forward svc/nebula-graphd 3699
```

To access Nebula through Graph Studio, run

```bash
kubectl port-forward svc/nebula-graphd 7001:80
```

then open the UI in your browser at [http://localhost:7001](http://localhost:7001/?lang=EN_US) 
and use the following configuration to log in:

- Host: `nebula-graphd:3699`
- User: `user` (literally)
- Password: `password` (literally)
