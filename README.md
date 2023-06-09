# SYS_6-06
Kubernetes. Часть 2
## Задание 1
Выполните действия:
1. Создайте свой кластер с помощью kubeadm.
2. Установите любой понравившийся CNI плагин.
3. Добейтесь стабильной работы кластера.
4. В качестве ответа пришлите скриншот результата выполнения команды ``` kubectl get po -n kube-system ```.
### Ответ:
![6-06_1 1](https://github.com/Roman-Teterevlev/SYS_6-06/assets/132853752/20f181e5-cea6-4799-ace0-c2400d681023)
![6-06_1 2](https://github.com/Roman-Teterevlev/SYS_6-06/assets/132853752/bcff1759-646b-4516-a592-636955eb096c)
![6-06_1 3](https://github.com/Roman-Teterevlev/SYS_6-06/assets/132853752/c150d06e-9ce9-4300-bc8b-cc78d87a7c84)
## Задание 2

Есть файл с деплоем:
```
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis
spec:
  selector:
    matchLabels:
      app: redis
  replicas: 1
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
      - name: master
        image: bitnami/redis
        env:
         - name: REDIS_PASSWORD
           value: password123
        ports:
        - containerPort: 6379
```
Выполните действия:
1. Создайте Helm Charts.
2. Добавьте в него сервис.
3. Вынесите все нужные, на ваш взгляд, параметры в values.yaml.
4. Запустите чарт в своём кластере и добейтесь его стабильной работы.
5. В качестве ответа пришлите вывод команды ``` helm get manifest <имя_релиза> ```.
### Ответ:
![6-06_2 1](https://github.com/Roman-Teterevlev/SYS_6-06/assets/132853752/ba7127ea-f1e7-44e5-9bf5-484085de60b6)
![6-06_2 2](https://github.com/Roman-Teterevlev/SYS_6-06/assets/132853752/db1fe8e3-5589-4a51-96a3-734421264307)
![6-06_2 3](https://github.com/Roman-Teterevlev/SYS_6-06/assets/132853752/7094e593-7f07-4959-90dd-c0ae13a189dd)
```
---
# Source: rt606/templates/serviceaccount.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: rt606-1685458842
  labels:
    helm.sh/chart: rt606-0.1.0
    app.kubernetes.io/name: rt606
    app.kubernetes.io/instance: rt606-1685458842
    app.kubernetes.io/version: "1.16.0"
    app.kubernetes.io/managed-by: Helm
---
# Source: rt606/templates/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: redis
spec:
  selector:
    app: redis
  ports:
    - protocol: TCP
      port: 6379
      targetPort: 6379
---
# Source: rt606/templates/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis
spec:
  selector:
    matchLabels:
      app: redis
  replicas: 1
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
      - name: master
        image: bitnami/redis
        env:
         - name: REDIS_PASSWORD
           value: password123
        ports:
         - containerPort: 6379
```
