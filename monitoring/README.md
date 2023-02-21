# Install monitoring

### Kube-state-metrics
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install kube-state-metrics charts/ksm --create-namespace --namespace monitoring
```
### Node-exporter
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install node-exporter charts/nexporter --create-namespace --namespace monitoring
```
### Victoriametrics
```
helm repo add vm https://victoriametrics.github.io/helm-charts/
helm repo update
helm install victoriametrics charts/vm -f charts/vm/my-values.yaml
```
