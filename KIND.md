# Local Development using Kind

## Setting up a cluster for Nebula

Install kind as described [here](https://kind.sigs.k8s.io/docs/user/quick-start/), then create
a new Kubernetes cluster called `nebula` like so:

```
kind create cluster --name nebula
```

You should be presesnted with output similar to the following:

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

## Switching to the cluster

```bash
kubectl cluster-info --context kind-nebula
```
