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

На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.
Ответить в свободной форме.

Решение 1

В режиме репликации master-slave у нас есть один главный сервер (master), который принимает записи и распространяет их на один или несколько вспомогательных серверов (slave). Таким образом, все изменения данных происходят на master-сервере и потом только передаются на slave-серверы. А вот в режиме репликации master-master оба сервера имеют возможность принимать и обрабатывать записи, а затем синхронизировать их между собой. Это позволяет балансировать нагрузку и обеспечивает отказоустойчивость. В обоих случаях цель - обеспечить отказоустойчивость и повысить производительность системы

###Задание 2

Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.
Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.

Решение 2


Предворительно устанавливаем docker:

curl -fsSL https://get.docker.com -o get-docker.sh

$ sudo sh get-docker.sh

Executing docker install script, commit: 7cae5f8b0decc17d6571f9f52eb840fbc13b2737

<...>

sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo usermod -aG docker $USER 

newgrp docker

systemctl status docker

После устанавливаем Visual Studio Code и выполняем работу в нем.

Открываем меню с помощью F1 или комбинацию клавиш Ctrl-Shift-P и вводим фразу “Configure Display Language” и выбираем русский язык, перезапускаем в VS code.

устанавливаем расширение для docker .

после открываем терминал (Ctrl + ‘) и вводим команды:

docker run -d --name replication-master -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.3

docker run -d --name replication-slave -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.3

docker network create replication

docker network connect replication replication-master

docker network connect replication replication-slave

после заходим в файл который находится в replication-master по пути /etc/my.cnf и вносим следующие изменения после строки [mysqld]:

server_id = 1

log_bin = mysql-bin

И перезапускаем контейнер 

Также мы делаем в replication-slave но вносим после [mysqld]:

server_id = 2

log_bin = mysql-bin

relay-log = /var/lib/mysql/mysql-relay-bin

relay-bin = /var/lib/mysql/mysql-relay-bin.index

read_only = 1

И перезапускаем контейнер, после чего запускаем терминалы на обоих контейнерах и заходим в базу под пользователем root:

mysql -u root -p

![1]()

Далее создаем пользователя на master и выдаем ему права:

CREATE USER 'replication'@'%';

GRANT REPLICATION SLAVE ON *.* TO 'replication'@'%';

SHOW GRANTS FOR replication@'%';

![2]()

SHOW MASTER STATUS;

![3]()

Далее на slave выполняем команды, в которых необходимо указать фай и позицию как на скрине выше:

CHANGE MASTER TO

-> MASTER_HOST='replication-master',

-> MASTER_USER='replication', MASTER_LOG_FILE='mysql-bin.000004',

-> MASTER_LOG_POS=158;

![4]()

START REPLICA;

SHOW SLAVE STATUS\G

![5]()

Проверяем что ошибок нет

Создаем в master базу данных:

CREATE database sakila;

show databases;

![6]()

И проверяем что она копировалась на slave

![7]()

После создаем таблицу в базе данных sakila на master

CREATE TABLE actor (

-> actor_id SMALLINT UNSIGNED NOT NULL AUTO_INCREMENT,

-> first_name VARCHAR(45) NOT NULL,

-> last_name VARCHAR(45) NOT NULL,

-> last_update TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

-> PRIMARY KEY (actor_id)

-> ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

![8]()

show tables;

![9]()

И проверяем что таблица появилась на slave

![10]()