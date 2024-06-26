# Домашнее задание к занятию «Хранение в K8s. Часть 1» - Черепанов Владислав

### Цель задания

В тестовой среде Kubernetes нужно обеспечить обмен файлами между контейнерам пода и доступ к логам ноды.

------

### Чеклист готовности к домашнему заданию

1. Установленное K8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключенным GitHub-репозиторием.

------

### Дополнительные материалы для выполнения задания

1. [Инструкция по установке MicroK8S](https://microk8s.io/docs/getting-started).
2. [Описание Volumes](https://kubernetes.io/docs/concepts/storage/volumes/).
3. [Описание Multitool](https://github.com/wbitt/Network-MultiTool).

------

### Задание 1 

**Что нужно сделать**

Создать Deployment приложения, состоящего из двух контейнеров и обменивающихся данными.

1. Создать Deployment приложения, состоящего из контейнеров busybox и multitool.  
[deployment.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/2.1/object/deployment.yaml "Деплой") 
2. Сделать так, чтобы busybox писал каждые пять секунд в некий файл в общей директории.  
  
Использовал команду watch, с записью даты и времени в файл.
```bash
command: [ 'sh', '-c', 'watch -n 5 date > /output/success.txt' ]
```  
Посмотрел видео в записи, услышал что необходимо что бы данные писались новой строкой для этого использую итератор ">>"  
```bash
command: [ 'sh', '-c', 'while true; do date >> /output/success.txt; sleep 3; done;' ]
```  
3. Обеспечить возможность чтения файла контейнером multitool.  

Входим в контейнеры pod's:  
```bash
kubectl exec -it pods/multitool-576c69f796-c2wvc  -c busybox -- sh
kubectl exec -it pods/multitool-576c69f796-c2wvc  -c multitool -- sh
```  

4. Продемонстрировать, что multitool может читать файл, который периодоически обновляется.  
<p align="center">
  <img src="https://github.com/plusvaldis/kuber-homeworks/blob/main/2.1/img/tail.gif">
</p>  
  
<p align="center">
  <img src="https://github.com/plusvaldis/kuber-homeworks/blob/main/2.1/img/tail_1.gif">
</p>  
5. Предоставить манифесты Deployment в решении, а также скриншоты или вывод команды из п. 4.

------

### Задание 2

**Что нужно сделать**

Создать DaemonSet приложения, которое может прочитать логи ноды.

1. Создать DaemonSet приложения, состоящего из multitool.  
[ddaemonset.yaml](https://github.com/plusvaldis/kuber-homeworks/blob/main/2.1/object/daemonset.yaml "daemon") 
2. Обеспечить возможность чтения файла `/var/log/syslog` кластера MicroK8S.  
Предоставил права на чтение с помощью команды, на файл  
```bash
chmod 644 /var/log/syslog
```
3. Продемонстрировать возможность чтения файла изнутри пода.  
<p align="center">
  <img src="https://github.com/plusvaldis/kuber-homeworks/blob/main/2.1/img/daemon.gif">
</p>  
4. Предоставить манифесты Deployment, а также скриншоты или вывод команды из п. 2.

------

### Правила приёма работы

1. Домашняя работа оформляется в своём Git-репозитории в файле README.md. Выполненное задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl`, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.

------
