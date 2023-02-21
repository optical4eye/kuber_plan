# Kuber plan

## Список проектов
<br />

- [ArgoCD](./argo_cd) - Манифесты установки ArgoCD

- [Persistent volume nfs](./dynamic-pv) - Создание динамического PV на nfs

- [Helm chart](./helm) - Создание простого чарта и публикация его на github

- [Monitoring](./monitoring) - Манифесты для развертывания мониторинга (victoriametrics, node-exporter, vm-agent)

- [Resourcequota](./resourcequota) - Манифесты для создания квот

- [StatefullSet](./statefullset) - Пример создания StatefullSet

<br />

## Команды
<br />

- ### Инфо о поде
```
kubectl describe --namespace open-app pod open-app-5855bdb497-gdhcz
```
- ### Логи пода
```
kubectl logs --namespace open-app open-app-5855bdb497-gdhcz -f
```
- ### Краткое инфо о поде
```
kubectl get pod --namespace open-app open-app-5855bdb497-gdhcz -o wide
```
- ### Convert file to base64
```
gzip -c test.tx | base64 > test.txt.gz.b64

base64 -d test.txt.gz.b64 > test.txt.gz

gunzip test.txt.gz
```

