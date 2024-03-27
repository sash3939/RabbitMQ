# Домашнее задание к занятию  «Очереди RabbitMQ»

---

### Задание 1. Установка RabbitMQ

Используя Vagrant или VirtualBox, создайте виртуальную машину и установите RabbitMQ.
Добавьте management plug-in и зайдите в веб-интерфейс.

*Итогом выполнения домашнего задания будет приложенный скриншот веб-интерфейса RabbitMQ.*

---
### Решение 1. Установка RabbitMQ
[rabbit](https://github.com/sash3939/RabbitMQ/assets/156709540/b5a23b68-f34e-4b8f-a7a5-f642265f6328)

---
### Задание 2. Отправка и получение сообщений

Используя приложенные скрипты, проведите тестовую отправку и получение сообщения.
Для отправки сообщений необходимо запустить скрипт producer.py.

Для работы скриптов вам необходимо установить Python версии 3 и библиотеку Pika.
Также в скриптах нужно указать IP-адрес машины, на которой запущен RabbitMQ, заменив localhost на нужный IP.

```shell script
$ pip install pika
```

Зайдите в веб-интерфейс, найдите очередь под названием hello и сделайте скриншот.
После чего запустите второй скрипт consumer.py и сделайте скриншот результата выполнения скрипта

*В качестве решения домашнего задания приложите оба скриншота, сделанных на этапе выполнения.*

Для закрепления материала можете попробовать модифицировать скрипты, чтобы поменять название очереди и отправляемое сообщение.

---
### Решение 2. Отправка и получение сообщений
[hello](https://github.com/sash3939/RabbitMQ/assets/156709540/951f24c2-6939-4cdc-9cf3-1898c16ac239)
[get message](https://github.com/sash3939/RabbitMQ/assets/156709540/6d2d58c2-a994-4ae9-9bca-355eef97f1a7)
[consumer](https://github.com/sash3939/RabbitMQ/assets/156709540/9a98aaa3-17e8-4fc0-9fa7-eb5790f1dd1a)
[other name queue and message](https://github.com/sash3939/RabbitMQ/assets/156709540/ccddb28f-ca52-4521-8a90-93ae8fa75ce4)
---

### Задание 3. Подготовка HA кластера

Используя Vagrant или VirtualBox, создайте вторую виртуальную машину и установите RabbitMQ.
Добавьте в файл hosts название и IP-адрес каждой машины, чтобы машины могли видеть друг друга по имени.

Пример содержимого hosts файла:
```shell script
$ cat /etc/hosts
192.168.0.10 rmq01
192.168.0.11 rmq02
```
После этого ваши машины могут пинговаться по имени.

Затем объедините две машины в кластер и создайте политику ha-all на все очереди.

*В качестве решения домашнего задания приложите скриншоты из веб-интерфейса с информацией о доступных нодах в кластере и включённой политикой.*

Также приложите вывод команды с двух нод:

```shell script
$ rabbitmqctl cluster_status
```

Для закрепления материала снова запустите скрипт producer.py и приложите скриншот выполнения команды на каждой из нод:

```shell script
$ rabbitmqadmin get queue='hello'
```

После чего попробуйте отключить одну из нод, желательно ту, к которой подключались из скрипта, затем поправьте параметры подключения в скрипте consumer.py на вторую ноду и запустите его.

*Приложите скриншот результата работы второго скрипта.*

[policy-cli](https://github.com/sash3939/RabbitMQ/assets/156709540/13831118-ac0d-401f-a79d-e0db59eb8ee3)
[policy-web](https://github.com/sash3939/RabbitMQ/assets/156709540/e689e9b4-9582-425a-a915-20bc6a7a505d)
[cluster-cli](https://github.com/sash3939/RabbitMQ/assets/156709540/fc5c5dc2-4706-4e40-b4fb-8bcb4b540a21)
[cluster-web](https://github.com/sash3939/RabbitMQ/assets/156709540/7108f24c-3384-41d2-a09b-557f338ec2ae)
[cluster_status rabbitmq1](https://github.com/sash3939/RabbitMQ/assets/156709540/74785429-7805-40d8-93d3-905b098a3de6)
[cluster_status rabbitmq2](https://github.com/sash3939/RabbitMQ/assets/156709540/b6c9153c-16a9-4a30-ac7f-8b8a9af1cfe0)
[cluster_status rabbitmq3](https://github.com/sash3939/RabbitMQ/assets/156709540/4899bcb7-bfd8-48b5-b645-2bfb07510e6e)

сообщения получаются, но в cli нет доступа к API Management, права по умолчанию. В целом функционал HA работает 
[hello](https://github.com/sash3939/RabbitMQ/assets/156709540/293ebbf0-f601-4ae3-bf05-dd78fb40595f)




## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### * Задание 4. Ansible playbook

Напишите плейбук, который будет производить установку RabbitMQ на любое количество нод и объединять их в кластер.
При этом будет автоматически создавать политику ha-all.

*Готовый плейбук разместите в своём репозитории.*
### * Решение 4. Ansible playbook

[playbook](https://github.com/sash3939/RabbitMQ/assets/156709540/259da21d-f354-4576-84c9-6879a7fb2884)


---

    - name: Создание политики ha-all
      command: rabbitmqctl set_policy ha-all "" '{"ha-mode":"all"}'

