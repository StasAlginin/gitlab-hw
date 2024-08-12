# Домашнее задание к занятию "`Название занятия`" - `Фамилия и имя студента`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

Используя Vagrant или VirtualBox, создайте виртуальную машину и установите RabbitMQ. Добавьте management plug-in и зайдите в веб-интерфейс.

Итогом выполнения домашнего задания будет приложенный скриншот веб-интерфейса RabbitMQ.

### Решение 1

Создаем директорию для проекта:

sudo mkdir REBBITMQ

cd REBBITMQ

Далее создаем файлы:

sudo nano docker-compose.yml

version: '3.8'

services:

 rabbitmq1:

   image: rabbitmq:3.10.7-management

   hostname: rabbitmq1

   environment:

     - RABBITMQ_DEFAULT_USER=${RABBITMQ_DEFAULT_USER}

     - RABBITMQ_DEFAULT_PASS=${RABBITMQ_DEFAULT_PASS}

     - RABBITMQ_CONFIG_FILE=/config/rabbitmq

     - RABBITMQ_ERLANG_COOKIE=${RABBITMQ_ERLANG_COOKIE}

     - RABBITMQ_NODE_PORT=5672

   volumes:

     - ./config:/config

   ports:

     - 15672:15672

     - 5672:5672


Так же создаем директорию config и в ней файл rabbitmq.conf:

loopback_users.guest = false

cluster_formation.peer_discovery_backend = rabbit_peer_discovery_classic_config

cluster_formation.classic_config.nodes.1 = rabbit@rabbitmq1

mnesia_table_loading_retry_timeout = 10000

mnesia_table_loading_retry_limit = 2


И файл .env_example:

RABBITMQ_DEFAULT_USER=test

RABBITMQ_DEFAULT_PASS=mytest

RABBITMQ_DEFAULT_COOKIE=12345



после переходим на веб интерфейс

![]()


### Задание 2

Используя приложенные скрипты, проведите тестовую отправку и получение сообщения. Для отправки сообщений необходимо запустить скрипт producer.py.

Для работы скриптов вам необходимо установить Python версии 3 и библиотеку Pika. Также в скриптах нужно указать IP-адрес машины, на которой запущен RabbitMQ, заменив localhost на нужный IP.

$ pip install pika

Зайдите в веб-интерфейс, найдите очередь под названием hello и сделайте скриншот. После чего запустите второй скрипт consumer.py и сделайте скриншот результата выполнения скрипта

В качестве решения домашнего задания приложите оба скриншота, сделанных на этапе выполнения.

Для закрепления материала можете попробовать модифицировать скрипты, чтобы поменять название очереди и отправляемое сообщение.


### Решение 2

sudo apt install python3

sudo apt install python3-pip

pip install pika

sudo apt install python3-pika

sudo apt install python-pika-doc

sudo mkdir demo

sudo nano consumer.py

Вносим:

#!/usr/bin/env python

# coding=utf-8

import pika


connection = pika.BlockingConnection(pika.ConnectionParameters('172.16.17.206'))

channel = connection.channel()

channel.queue_declare(queue='hello')


def callback(ch, method, properties, body):

print(" [x] Received %r" % body)


channel.basic_consume(callback, queue='hello', no_ack=True)

channel.start_consuming()


После:

sudo nano producer.py

Вносим:

#!/usr/bin/env python

# coding=utf-8

import pika


connection = pika.BlockingConnection(pika.ConnectionParameters('172.16.17.206', credentials=pika.PlainCredentials('test', 'mytest')))

channel = connection.channel()

channel.queue_declare(queue='hello')

channel.basic_publish(exchange='', routing_key='hello', body='Hello Netology!')

connection.close()


После: 

cd demo

source env/bin/activate

sudo python producer.py

![2]()

![3]()

![4]()

### Задание 3

Используя Vagrant или VirtualBox, создайте вторую виртуальную машину и установите RabbitMQ. Добавьте в файл hosts название и IP-адрес каждой машины, чтобы машины могли видеть друг друга по имени.

Пример содержимого hosts файла:

$ cat /etc/hosts

192.168.0.10 rmq01

192.168.0.11 rmq02

После этого ваши машины могут пинговаться по имени.

Затем объедините две машины в кластер и создайте политику ha-all на все очереди.

В качестве решения домашнего задания приложите скриншоты из веб-интерфейса с информацией о доступных нодах в кластере и включённой политикой.

Также приложите вывод команды с двух нод:

$ rabbitmqctl cluster_status

Для закрепления материала снова запустите скрипт producer.py и приложите скриншот выполнения команды на каждой из нод:

$ rabbitmqadmin get queue='hello'

После чего попробуйте отключить одну из нод, желательно ту, к которой подключались из скрипта, затем поправьте параметры подключения в скрипте consumer.py на вторую ноду и запустите его.

Приложите скриншот результата работы второго скрипта.


### Решение 3

Объединяем машины:

Docer compose.yml

version: '3.8'

services:

 rabbitmq1:

   image: rabbitmq:3.10.7-management

   hostname: rabbitmq1

   environment:

     - RABBITMQ_DEFAULT_USER=test

     - RABBITMQ_DEFAULT_PASS=mytest

     - RABBITMQ_CONFIG_FILE=/config/rabbitmq

     - RABBITMQ_ERLANG_COOKIE=12345

     - RABBITMQ_NODE_PORT=5672

   volumes:

     - ./config:/config

   ports:

     - 15672:15672

     - 5672:5672

  rabbitmq2:

   image: rabbitmq:3.10.7-management

   hostname: rabbitmq2

   environment:

     - RABBITMQ_DEFAULT_USER=test

     - RABBITMQ_DEFAULT_PASS=mytest

     - RABBITMQ_CONFIG_FILE=/config/rabbitmq

     - RABBITMQ_ERLANG_COOKIE=12345

     - RABBITMQ_NODE_PORT=5672

   volumes:

     - ./config:/config

  rabbitmq3:

   image: rabbitmq:3.10.7-management

   hostname: rabbitmq3

   environment:

     - RABBITMQ_DEFAULT_USER=test

     - RABBITMQ_DEFAULT_PASS=mytest

     - RABBITMQ_CONFIG_FILE=/config/rabbitmq

     - RABBITMQ_ERLANG_COOKIE=12345

     - RABBITMQ_NODE_PORT=5672

   volumes:

     - ./config:/config

rabbitmq.conf

loopback_users.guest = false

cluster_formation.peer_discovery_backend = rabbit_peer_discovery_classic_config

cluster_formation.classic_config.nodes.1 = rabbit@rabbitmq1

cluster_formation.classic_config.nodes.2 = rabbit@rabbitmq2

cluster_formation.classic_config.nodes.3 = rabbit@rabbitmq3

mnesia_table_loading_retry_timeout = 10000

mnesia_table_loading_retry_limit = 2

![5]()

![6]()

Создание кластера:

![7]()

Вывод команды  rabbitmqctl cluster_status на 2х машинах:

rabbitmqctl cluster_status

RABBITMQ_ERLANG_COOKIE env variable support is deprecated and will be REMOVED in a future version. Use the $HOME/.erlang.cookie file or the --erlang-cookie switch instead.

Cluster status of node rabbit@rabbitmq1 ...

Basics


Cluster name: rabbit@rabbitmq1


Disk Nodes


rabbit@rabbitmq1

rabbit@rabbitmq2

rabbit@rabbitmq3


Running Nodes


rabbit@rabbitmq1

rabbit@rabbitmq2

rabbit@rabbitmq3


Versions


rabbit@rabbitmq1: RabbitMQ 3.10.7 on Erlang 25.0.4

rabbit@rabbitmq2: RabbitMQ 3.10.7 on Erlang 25.0.4

rabbit@rabbitmq3: RabbitMQ 3.10.7 on Erlang 25.0.4


Maintenance status


Node: rabbit@rabbitmq1, status: not under maintenance

Node: rabbit@rabbitmq2, status: not under maintenance

Node: rabbit@rabbitmq3, status: not under maintenance


Alarms


(none)


Network Partitions


(none)


Listeners


Node: rabbit@rabbitmq1, interface: [::], port: 15672, protocol: http, purpose: HTTP API

Node: rabbit@rabbitmq1, interface: [::], port: 15692, protocol: http/prometheus, purpose: Prometheus exporter API over HTTP

Node: rabbit@rabbitmq1, interface: [::], port: 25672, protocol: clustering, purpose: inter-node and CLI tool communication

Node: rabbit@rabbitmq1, interface: [::], port: 5672, protocol: amqp, purpose: AMQP 0-9-1 and AMQP 1.0

Node: rabbit@rabbitmq2, interface: [::], port: 15672, protocol: http, purpose: HTTP API

Node: rabbit@rabbitmq2, interface: [::], port: 15692, protocol: http/prometheus, purpose: Prometheus exporter API over HTTP

Node: rabbit@rabbitmq2, interface: [::], port: 25672, protocol: clustering, purpose: inter-node and CLI tool communication

Node: rabbit@rabbitmq2, interface: [::], port: 5672, protocol: amqp, purpose: AMQP 0-9-1 and AMQP 1.0

Node: rabbit@rabbitmq3, interface: [::], port: 15672, protocol: http, purpose: HTTP API

Node: rabbit@rabbitmq3, interface: [::], port: 15692, protocol: http/prometheus, purpose: Prometheus exporter API over HTTP

Node: rabbit@rabbitmq3, interface: [::], port: 25672, protocol: clustering, purpose: inter-node and CLI tool communication

Node: rabbit@rabbitmq3, interface: [::], port: 5672, protocol: amqp, purpose: AMQP 0-9-1 and AMQP 1.0

Feature flags


Flag: classic_mirrored_queue_version, state: enabled

Flag: drop_unroutable_metric, state: enabled

Flag: empty_basic_get_metric, state: enabled

Flag: implicit_default_bindings, state: enabled

Flag: maintenance_mode_status, state: enabled

Flag: quorum_queue, state: enabled

Flag: stream_queue, state: enabled

Flag: user_limits, state: enabled

Flag: virtual_host_metadata, state: enabled

![8]()

![9]()

Удаляем 1 из нод в созданной до этого My_exchange

![10]()

И редактируем consume.py

#!/usr/bin/env python

# coding=utf-8

import pika


connection = pika.BlockingConnection(pika.ConnectionParameters('172.16.17.206', credentials=pika.PlainCredentials('test', 'mytest')))

channel = connection.channel()

channel.queue_declare(queue='hello')


channel.queue_bind(exchange='My_exchange', queue='My_VM1')


def callback(ch, method, properties, body):

   print(" [x] Received %r" % body)




channel.basic_consume(queue='My_VM1', on_message_callback=callback, auto_ack=True)

channel.start_consuming()


Вывод команды sudo python consumer.py

![11]()

После мы видим что на 1VM запросы исчезли, а на 2VM остались

![12]()