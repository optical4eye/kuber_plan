# Helm

### Создать chart
```
helm create openresty-art
```
### Проверить генерацию темплейта
```
helm template app  ./openresty-art/ > tets_deploy.yml
```
### Установить chart из локальной дирректории
```
helm install open-app --create-namespace --namespace open-app ./openresty-art/
```
### Запаковать chart
```
helm package openresty-art/
```
### Создать index.yml с версиями
```
helm repo index . --url https://raw.githubusercontent.com/optical4eye/kuber_plan/main/helm/chart
```
### Добавляем chart в helm repo
```
helm repo add openresty-art https://raw.githubusercontent.com/optical4eye/kuber_plan/main/helm/chart
helm repo update
helm repo list
helm search repo --versions | grep openresty-art
helm list --all-namespaces
```