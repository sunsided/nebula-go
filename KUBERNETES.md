# Nebula Graph Kubernetes Deployment

Please find the information in [How to Deploy Nebula Graph on Kubernetes](https://nebula-graph.io/posts/how-to-deploy-nebula-graph-in-kubernetes/).

The Helm chart is taken from the official repository [vesoft-inc/nebula/kubernetes/helm](https://github.com/vesoft-inc/nebula/tree/master/kubernetes/helm).

## Deploy

### Software And Hardware Requirements

The following list is software and hardware requirements involved in the deployment in the post
linked above:

- The operation system is CentOS-7.6.1810 x86_64.
- Virtual machine configuration:
  - 4 CPU
  - 8G memory
  - 50G system disk
  - 50G data disk A
  - 50G data disk B
- Kubernetes cluster is version v1.16.
- Use local PV as data storage.

### Cluster Topology

Following is the cluster topology:


| Server IP   | Nebula Services             | Role       |
|-------------|-----------------------------|------------|
| 192.168.0.1 |                             | k8s-master |
| 192.168.0.2 | graphd, metad-0, storaged-0 | k8s-slave  |
| 192.168.0.3 | graphd, metad-1, storaged-1 | k8s-slave  |
| 192.168.0.4 | graphd, metad-2, storaged-2 | k8s-slave  |

## Local Development using Kind

### Setting up a cluster for Nebula

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

### Switching to the cluster

```bash
kubectl cluster-info --context kind-nebula
kubectl config use-context kind-nebula
```

### Installing the Helm chart

Make sure to select the correct Kubernetes context by either using `kubectl config use-context kind-nebula` or by specifying the `--kube-context=kind-nebula` to Helm.


```bash
kubectl config use-context kind-nebula
helm install nebula helm/ # WARNING! You'll need to add options to apply your configuration!
helm list
```

This will spin up the appropriate pods using the default configuration