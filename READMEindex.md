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

Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.


Решение 1

SELECT 

    SUM(sum_value_table.index_size) * 100 / SUM(sum_value_table.table_size) AS index_size_percent

FROM

    (SELECT 

        SUM(index_length) AS index_size, SUM(data_length) AS table_size

    FROM

        information_schema.tables

    WHERE

        table_schema = 'sakila') AS sum_value_table;


![1](https://github.com/StasAlginin/gitlab-hw/blob/main/img/index1.jpeg)


### Задание 2

Выполните explain analyze следующего запроса:

select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id, f.title)

from payment p, rental r, customer c, inventory i, film f

where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id

1) перечислите узкие места;

2) оптимизируйте запрос: внесите корректировки по использованию операторов, при необходимости добавьте индексы.


Решение 2

1) Узкие места в запросе: отсутствие явного указания связей между таблицами (например, связь film_id между таблицами inventory и film), использование старого синтаксиса соединений через запятые.


2) Оптимизированный запрос:

EXPLAIN ANALYZE

SELECT DISTINCT CONCAT(c.last_name, ' ', c.first_name), 

                SUM(p.amount) OVER (PARTITION BY c.customer_id, f.title)

FROM payment p

JOIN rental r ON p.payment_date = r.rental_date

JOIN customer c ON r.customer_id = c.customer_id

JOIN inventory i ON i.inventory_id = r.inventory_id

JOIN film f ON i.film_id = f.film_id

WHERE p.payment_date >= '2005-07-30' AND p.payment_date < DATE_ADD('2005-07-30', INTERVAL 1 DAY);

![2](https://github.com/StasAlginin/gitlab-hw/blob/main/img/index2.jpeg)


