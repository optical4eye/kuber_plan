# Helm

### Создать chart


```
helm create openresty-art
```

### Проверить генерацию темплейта

helm template app  ./openresty-art/ > tets_deploy.yml

helm install open-app --create-namespace --namespace open-app ./openresty-art/
