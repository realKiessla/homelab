# Argo CD
Currently, Argo CD doesn't support ARM64 architecture. Therefore, we have to use our own `install.yaml` with replaced images.

## Installation
```
kubectl create namespace argocd
kubectl apply -n argocd -f install.yaml
```

After a successful installation we can install our `ingress` route:
```
kubectl apply -n argocd -f ingress.yaml
```
