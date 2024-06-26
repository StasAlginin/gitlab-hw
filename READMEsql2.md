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

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

фамилия и имя сотрудника из этого магазина;

город нахождения магазина;

количество пользователей, закреплённых в этом магазине.


Решение 1

SELECT 

    staff.first_name,

    staff.last_name,

    city.city,

    COUNT(customer.customer_id) AS customer_count

FROM store

JOIN staff ON store.store_id = staff.store_id

JOIN address ON store.address_id = address.address_id

JOIN city ON address.city_id = city.city_id

JOIN customer ON store.store_id = customer.store_id

GROUP BY staff.first_name, staff.last_name, city.city

HAVING COUNT(customer.customer_id) > 300;


![1](https://github.com/StasAlginin/gitlab-hw/blob/main/img/sql2(1).jpeg)


### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

Решение 2

SELECT COUNT(*) AS film_count

FROM film

WHERE length > (SELECT AVG(length) FROM film);

![2](https://github.com/StasAlginin/gitlab-hw/blob/main/img/sql2(2).jpeg)


### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

Решение 3

SELECT 

    DATE_FORMAT(payment.payment_date, '%Y-%m') AS payment_month,

    COUNT(rental.rental_id) AS rental_count

FROM payment

JOIN rental ON payment.rental_id = rental.rental_id

GROUP BY payment_month

ORDER BY SUM(amount) DESC

LIMIT 1;

![3](https://github.com/StasAlginin/gitlab-hw/blob/main/img/sql2(3).jpeg)

