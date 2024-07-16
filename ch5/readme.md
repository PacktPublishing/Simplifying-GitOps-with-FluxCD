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
  --path=ch5/flux-cluster/packt-fluxcd \
  --namespace=flux-system \
  --components-extra image-reflector-controller,image-automation-controller
```

## How to setup kube-proxy for accessing prometheus?
```bash
kubectl -n monitoring port-forward svc/kube-prometheus-stack-prometheus  9090:9090 
```

## How to setup kube-proxy for accessing grafana?

```bash
kubectl -n monitoring port-forward svc/kube-prometheus-stack-grafana 3000:80
```
