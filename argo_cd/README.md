# Install Argo CD

### Install Argo
```
kubectl create namespace argocd
kubectl apply -n argocd -f argocd.yml
```
### Apply ingress
```
kubectl apply -n argocd -f ingress.yml

```
### Argo CD CLI
```
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
```
### Argo set new admin pass
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d ; echo
argocd login argo.cluster.local:30443 --grpc-web
argocd account update-password --grpc-web
```