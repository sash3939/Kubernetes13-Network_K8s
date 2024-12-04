# Домашнее задание к занятию «Как работает сеть в K8s»

### Цель задания

Настроить сетевую политику доступа к подам.

### Чеклист готовности к домашнему заданию

1. Кластер K8s с установленным сетевым плагином Calico.

<img width="577" alt="Calico" src="https://github.com/user-attachments/assets/d2827b5c-78ba-4cbd-a5d3-f01938f5e93a">


### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Документация Calico](https://www.tigera.io/project-calico/).
2. [Network Policy](https://kubernetes.io/docs/concepts/services-networking/network-policies/).
3. [About Network Policy](https://docs.projectcalico.org/about/about-network-policy).

-----

### Задание 1. Создать сетевую политику или несколько политик для обеспечения доступа

1. Создать deployment'ы приложений frontend, backend и cache и соответсвующие сервисы.

[deployment-front](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/deployment-front.yaml)

[deployment-back](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/deployment-back.yaml)

[deployment-cache](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/deployment-cache.yaml)

[svc-front](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/svc-front.yaml)

[svc-back](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/svc-back.yaml)

[svc-cache](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/svc-cache.yaml)

<img width="515" alt="deployment and services" src="https://github.com/user-attachments/assets/f354d572-467e-4708-b76d-4f414e6d8823">


2. В качестве образа использовать network-multitool.
3. Разместить поды в namespace App.
4. Создать политики, чтобы обеспечить доступ frontend -> backend -> cache. Другие виды подключений должны быть запрещены.
5. Продемонстрировать, что трафик разрешён и запрещён.

### Правила приёма работы

1. Домашняя работа оформляется в своём Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.
