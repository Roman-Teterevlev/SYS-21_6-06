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
