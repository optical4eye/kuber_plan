# Loki
helm install --namespace monitoring --values my-values.yaml loki grafana/loki --dry-run > manifest.yml