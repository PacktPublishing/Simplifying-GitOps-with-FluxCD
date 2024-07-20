# Generating Linkerd the certificates with step

Install step tool

```bash
brew install step
```

Generate Trust anchor certificate

```bash
step certificate create root.linkerd.cluster.local ca.crt ca.key --profile root-ca --no-password --insecure --not-after=87600h 
```

Generate issuer certificate and key 

```bash
step certificate create identity.linkerd.cluster.local issuer.crt issuer.key \
 > --profile intermediate-ca --not-after 87600h --no-password --insecure \
 > --ca ca.crt --ca-key ca.key
```

Create Kubernetes secrets linkerd-identity-issuer and linkerd-root-ca

```bash
### Create linkerd namespace
kubectl create ns linkerd
namespace/linkerd created

### Create linkerd-root-ca secret
kubectl create secret tls linkerd-root-ca --cert=ca.crt --key=ca.key --namespace=linkerd
secret/linkerd-root-ca created

### Create linkerd-identity-issuer secret
kubectl create secret tls linkerd-identity-issuer --cert=issuer.crt --key=issuer.key --namespace=linkerd
secret/linkerd-identity-issuer created
```