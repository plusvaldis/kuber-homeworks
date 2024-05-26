# Домашнее задание к занятию «Сетевое взаимодействие в K8S. Часть 2» - Черепанов Владислав

### Цель задания

В тестовой среде Kubernetes необходимо обеспечить доступ к двум приложениям снаружи кластера по разным путям.

------

### Чеклист готовности к домашнему заданию

1. Установленное k8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключённым Git-репозиторием.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Инструкция](https://microk8s.io/docs/getting-started) по установке MicroK8S.
2. [Описание](https://kubernetes.io/docs/concepts/services-networking/service/) Service.
3. [Описание](https://kubernetes.io/docs/concepts/services-networking/ingress/) Ingress.
4. [Описание](https://github.com/wbitt/Network-MultiTool) Multitool.

------

### Задание 1. Создать Deployment приложений backend и frontend

1. Создать Deployment приложения _frontend_ из образа nginx с количеством реплик 3 шт.  
[depl_front_nginx.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/object/depl_front_nginx.yaml "Деплой") 
2. Создать Deployment приложения _backend_ из образа multitool.  
[depl_back_multitool.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/object/depl_back_multitool.yaml "Деплой") 
3. Добавить Service, которые обеспечат доступ к обоим приложениям внутри кластера. 
[s_frontend.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/object/s_frontend.yaml "Service") 
[s_backend.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/object/s_backend.yaml "Service") 
4. Продемонстрировать, что приложения видят друг друга с помощью Service.  
![curl_1](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/img/back.png)
![curl_2](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/img/front.png)
5. Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.

------

### Задание 2. Создать Ingress и обеспечить доступ к приложениям снаружи кластера

1. Включить Ingress-controller в MicroK8S.  
```bash
kubectl create ns ingress-nginx  
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx  
helm repo update  
helm -n ingress-nginx install ingress-nginx ingress-nginx/ingress-nginx  
```
2. Создать Ingress, обеспечивающий доступ снаружи по IP-адресу кластера MicroK8S так, чтобы при запросе только по адресу открывался _frontend_ а при добавлении /api - _backend_.  
[ingress.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/object/ingress.yaml "ingress")  
3. Продемонстрировать доступ с помощью браузера или `curl` с локального компьютера.  
![ing](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/img/ing.png)  
![ng](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/img/ng.png)  
![ng_api](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.5/img/ng_api.png) 
4. Предоставить манифесты и скриншоты или вывод команды п.2.

------

### Правила приема работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl` и скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.

------
