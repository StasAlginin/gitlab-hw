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

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:

ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';


1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)


Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.



Решение 1

sudo apt install mysql-serve

sudo systemctl start mysql

sudo mysql

CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'Toporis1999';

SELECT user, host FROM mysql.user;

![1](https://github.com/StasAlginin/gitlab-hw/blob/main/img/rabotasdannimi1.jpeg)

RANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';

![2](https://github.com/StasAlginin/gitlab-hw/blob/main/img/rabotasdannimi2.jpeg)

EXIT;

mysql -u sys_temp -p

ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Toporis1999';

CREATE DATABASE sakila;

SHOW DATABASES;

![3](https://github.com/StasAlginin/gitlab-hw/blob/main/img/rabotasdannimi3.jpeg)

EXIT;

После скачиваем файлы из ссылки и извлекаем их в домашнюю директорию 

mysql -u sys_temp -p sakila < /home/algininss/sakila-db/sakila-schema.sql

mysql -u sys_temp -p sakila < /home/algininss/sakila-db/sakila-data.sql

mysql -u sys_temp -p sakila

SHOW TABLES;

![4](https://github.com/StasAlginin/gitlab-hw/blob/main/img/rabotasdannimi4.jpeg)


###Задание 2

Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)

Название таблицы | Название первичного ключа

   customer      | 	customer_id


Решение 2

SELECT table_name, column_name FROM information_schema.key_column_usage WHERE constraint_name = 'PRIMARY' AND table_schema = 'sakila';

![5](https://github.com/StasAlginin/gitlab-hw/blob/main/img/rabotasdannimi5.jpeg)
