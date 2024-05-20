# Домашнее задание к занятию «Запуск приложений в K8S» - Черепанов Владислав.

### Цель задания

В тестовой среде для работы с Kubernetes, установленной в предыдущем ДЗ, необходимо развернуть Deployment с приложением, состоящим из нескольких контейнеров, и масштабировать его.

------

### Чеклист готовности к домашнему заданию

1. Установленное k8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключённым git-репозиторием.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Описание](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) Deployment и примеры манифестов.
2. [Описание](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/) Init-контейнеров.
3. [Описание](https://github.com/wbitt/Network-MultiTool) Multitool.

------

### Задание 1. Создать Deployment и обеспечить доступ к репликам приложения из другого Pod

1. Создать Deployment приложения, состоящего из двух контейнеров — nginx и multitool. Решить возникшую ошибку.  
[depl_nginx.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/object/deploy.png "Деплой")  
2. После запуска увеличить количество реплик работающего приложения до 2.  
3. Продемонстрировать количество подов до и после масштабирования.  
![deploy](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/img/depl_nginx.png)  
4. Создать Service, который обеспечит доступ до реплик приложений из п.1.  
[service_depl.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/object/service_pod.yaml "Сервис_доступ") 
5. Создать отдельный Pod с приложением multitool и убедиться с помощью `curl`, что из пода есть доступ до приложений из п.1.  
[pod.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/object/pod.yaml "Pod")
```bash
kubectl exec --stdin --tty multitool -- /bin/bash
```  
![curl_1](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/img/curl_1.png)  
![curl_2](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/img/curl_2.png)  

------

### Задание 2. Создать Deployment и обеспечить старт основного контейнера при выполнении условий

1. Создать Deployment приложения nginx и обеспечить старт контейнера только после того, как будет запущен сервис этого приложения.  
[depl_nginx_busybox.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/object/depl_nginx_busybox.yaml "nginx init service")
2. Убедиться, что nginx не стартует. В качестве Init-контейнера взять busybox.  
![init](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/img/init.png)  
3. Создать и запустить Service. Убедиться, что Init запустился.  
[service_nginx_busybox.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/object/service_nginx_busybox.yaml "nginx service start")
4. Продемонстрировать состояние пода до и после запуска сервиса.  
![init](https://github.com/plusvaldis/kuber-homeworks/blob/main/1.3/img/service_init.png) 

------

### Правила приема работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl` и скриншоты результатов.
3. Репозиторий должен содержать файлы манифестов и ссылки на них в файле README.md.

------
