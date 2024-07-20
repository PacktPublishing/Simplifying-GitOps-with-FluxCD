# How to Install Local Kubernetes Cluster and Bootstrap FluxCD for Development Purposes

This guide shows how to set up a local Kubernetes cluster and bootstrap FluxCD for development purposes.

## Prerequisites

The local-k8s.yaml manifest for the Kubernetes cluster is available in the kind directory of this repository.

 ## Create a local kubernetes cluster

Use the following commands to install kind and create a local Kubernetes cluster:


```bash
brew install kind
```

Fork the GitHub repo https://github.com/grglzrv/simplifying-gitops-with-flux-cd.git and make sure to leave a star!

Clone the repository you forked and substitute <user> with your GitHub username.

```bash
git clone https://github.com/<user>/simplifying-gitops-with-flux-cd.git
cd fluxcd
kind create cluster --config ./kind/local-k8s.yaml --name <cluster-name>
```
To set the context for kubectl to your new cluster, use this alias:

```bash
alias kcc='kubectl config use-context'
kind get clusters
kcc <cluster-name>
```

## Bootstrap FluxCD

Here are the steps to bootstrap FluxCD on your local Kubernetes cluster

### Install the Flux CLI

Use the command below to install the Flux CLI. Remember to replace 2.3.0 with the version number you want to install.

```bash
curl -s https://fluxcd.io/install.sh | sudo FLUX_VERSION=2.3.0 bash
```

### Bootstrap Flux 

The `flux bootstrap` command can be used for the initial installation and for upgrades as well. See the example command below. Replace version for example - `v2.3.0` with the version number you want to install.

```bash
export GITHUB_TOKEN=<your-token>
flux bootstrap github --owner=<user> \
--repository=simplifying-gitops-with-flux-cd \
--components-extra=image-reflector-controller,image-automation-controller --version v2.3.0 \
--path=ch6/clusters/flagger \
--cluster-domain=cluster.local \
--branch=main \
--private=false \
--personal=true
```

Now you have a local Kubernetes cluster with FluxCD bootstrapped for your development work.