# create cluster with k3d
```bash
k3d cluster create -c k3d/packt-fluxcd.yaml
```

## How to install flux from git repo
```bash
flux bootstrap git \
  --url=ssh://git@github.com/116davinder/packt-fluxcd.git \
  --branch=main \
  --private-key-file=/home/pox/.ssh/id_rsa \
  --silent \
  --path=ch3/flux-cluster/packt-fluxcd \
  --namespace=flux-system \
  --components-extra image-reflector-controller,image-automation-controller
```

## How to install Jenkins?
Jenkins will be autoinstalled from `ch3/flux-cluster/packt-fluxcd/jenkins-*.yaml` files once 
fluxCD is bootstrapped.

## How to find Jenkins User and Password
* username: `admin`
* password

```bash
kubectl exec --namespace default -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo
```

## How to setup kube-proxy for accessing jenkins?

```
kubectl --namespace default port-forward svc/jenkins 8080:8080
```
