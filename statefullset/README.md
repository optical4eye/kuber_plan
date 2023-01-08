# Всякое про StatefullSet

## Stable Network ID

[Документация](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#stable-network-id).

Одна из особенностей StatefullSet является заранее определённое имя
пода, по которому мы можем к нему обратиться.

Для того, что бы это работало, в StatefullSet предусмотрен обязательный
headless service. При помощи которого определяется домен DNS, где
будут находиться имена подов.

Установим приложение.

```shell
kubectl apply -f stable-network-id
```

Что бы проверить как работает headless сервис, запустим приложение dnstools.

```shell
kubectl run -it --rm --restart=Never --image=infoblox/dnstools:latest dnstools
```

В появившейся консоли обратимся к DNS.

```shell
host application-0.application-headless.default.svc.cluster.local
host application-1.application-headless.default.svc.cluster.local
```

или

```shell
host application-0.application-headless.default.svc
host application-1.application-headless.default.svc
```

Убедимся, что полученные IP адреса соответствуют IP адресам подов.

Воспользуемся curl, что бы посмотреть какие данные будут выданы
при обращении к каждому поду.

```shell
curl application-0.application-headless.default.svc
curl application-1.application-headless.default.svc
```

Выйдем из dnstools

```shell
exit
```

## Pod Name Label

[Документация](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#pod-name-label).

К сожалению, конструкции headless сервиса нельзя использовать при
обращении к конкретному поду, например в ingress. Приведённый ниже пример
сгенерирует ошибку при попытке деплоя в кластер kubernetes.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: application
spec:
  ingressClassName: system-ingress
  rules:
  - host: app0.kryukov.local
    http:
      paths:
        - pathType: Prefix
          path: /
          backend:
            service:
              name: application-0.application-headless
              port:
                name: http
  - host: app1.kryukov.local
    http:
      paths:
        - pathType: Prefix
          path: /
          backend:
            service:
              name: application-1.application-headless
              port:
                name: http
```

Headless сервис - это записи в DNS, поэтому их можно использовать,
например при конфигурации приложений, там где необходимо сослаться
на приложение по имени.

Что делать, если к конкретному поду StatefulSet необходимо обратиться
при помощи сервиса?

При создании пода StatefullSet, контроллер автоматически добавляет
метку типа: `statefulset.kubernetes.io/pod-name`. Поэтому мы можем для
каждого пода создать отдельный сервис.

Автор: [Telegram](https://t.me/arturkryukov/95)