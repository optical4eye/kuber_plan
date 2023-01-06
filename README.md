# kuber_plan

### Инфо о поде
```
kubectl describe --namespace open-app pod open-app-5855bdb497-gdhcz
```
### Логи пода
```
kubectl logs --namespace open-app open-app-5855bdb497-gdhcz -f
```
### Краткое инфо о поде
```
kubectl get pod --namespace open-app open-app-5855bdb497-gdhcz -o wide
```
### convert file to base64
```
gzip -c test.tx | base64 > test.txt.gz.b64

base64 -d test.txt.gz.b64 > test.txt.gz

gunzip test.txt.gz
```