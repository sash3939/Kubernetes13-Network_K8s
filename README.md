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

```yaml
    spec:
      containers:
        - image: praqma/network-multitool:alpine-extra
          imagePullPolicy: IfNotPresent
          name: network-multitool
```

3. Разместить поды в namespace App.

<img width="362" alt="namespace app" src="https://github.com/user-attachments/assets/d25d5976-93d8-429b-8243-c995a59b3953">

4. Создать политики, чтобы обеспечить доступ frontend -> backend -> cache. Другие виды подключений должны быть запрещены.

Сначала покажу, что без политик никаких ограничений нет

<img width="655" alt="All allow" src="https://github.com/user-attachments/assets/495be3aa-1a97-4b94-a39d-ad023f1927a1">

Запретим все с помощью [network-policy-default](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/network-policy-default.yaml)

<img width="534" alt="default policy" src="https://github.com/user-attachments/assets/f2223742-12fb-4f1a-9b06-1e66bff21da5">

**Доступ frontend -> backend -> cache. Другие виды подключений должны быть запрещены
**

К frontend не можем подключиться [network-policy-front](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/network-policy-front.yaml)

К backend разрешено подключиться только с frontend [network-policy-back](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/network-policy-back.yaml)

К cache разрешено подключиться только backend [network-policy-cache](https://github.com/sash3939/Kubernetes13-Network_K8s/blob/main/network-policy-cache.yaml)

5. Продемонстрировать, что трафик разрешён и запрещён.

Проверка:

<img width="457" alt="policy deny" src="https://github.com/user-attachments/assets/e9a0186f-ba3b-4c60-bc19-94e7210ddf76">

<img width="572" alt="check policy" src="https://github.com/user-attachments/assets/2658b2bf-659e-454e-8e8d-a1e6dfddb303">


### Правила приёма работы

1. Домашняя работа оформляется в своём Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.
