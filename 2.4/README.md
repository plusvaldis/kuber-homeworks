# Домашнее задание к занятию «Управление доступом»  - Черепанов Владислав

### Цель задания

В тестовой среде Kubernetes нужно предоставить ограниченный доступ пользователю.

------

### Чеклист готовности к домашнему заданию

1. Установлено k8s-решение, например MicroK8S.
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключённым github-репозиторием.

------

### Инструменты / дополнительные материалы, которые пригодятся для выполнения задания

1. [Описание](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) RBAC.
2. [Пользователи и авторизация RBAC в Kubernetes](https://habr.com/ru/company/flant/blog/470503/).
3. [RBAC with Kubernetes in Minikube](https://medium.com/@HoussemDellai/rbac-with-kubernetes-in-minikube-4deed658ea7b).

------

### Задание 1. Создайте конфигурацию для подключения пользователя

1. Создайте и подпишите SSL-сертификат для подключения к кластеру.  
```bash
создаем закрытый ключ пользователя
openssl genrsa -out tester.key 2048
openssl req -new -key tester.key -out tester.csr -subj "/CN=tester"
openssl x509 -req -in /home/tester/tester.csr -CA /var/snap/microk8s/current/certs/ca.crt -CAkey /var/snap/microk8s/current/certs/ca.key -CAcreateserial -out /home/tester/tester.crt -days 500
mkdir .certs && mv tester.crt tester.key .certs
kubectl config set-credentials tester --client-certificate=/home/tester/.certs/tester.crt --client-key=/home/tester/.certs/tester.crt
kubectl config set-context tester-context --cluster=microk8s-cluster --user=tester  
microk8s enable rbac
```
2. Настройте конфигурационный файл kubectl для подключения.  
[config](https://github.com/plusvaldis/kuber-homeworks/blob/main/2.4/object/config "config")  
![access](https://github.com/plusvaldis/kuber-homeworks/blob/main/2.4/img/access.png)  
3. Создайте роли и все необходимые настройки для пользователя.  
[rolebindings](https://github.com/plusvaldis/kuber-homeworks/blob/main/2.4/object/rolebind.yaml "rolebindings")  
[role](https://github.com/plusvaldis/kuber-homeworks/blob/main/2.4/object/role.yaml "role")  
4. Предусмотрите права пользователя. Пользователь может просматривать логи подов и их конфигурацию (`kubectl logs pod <pod_id>`, `kubectl describe pod <pod_id>`).  
![access](https://github.com/plusvaldis/kuber-homeworks/blob/main/2.4/img/not_permitions.png)  
![access](https://github.com/plusvaldis/kuber-homeworks/blob/main/2.4/img/role.png) 
5. Предоставьте манифесты и скриншоты и/или вывод необходимых команд.

------

### Правила приёма работы

1. Домашняя работа оформляется в своём Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl`, скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.

------

