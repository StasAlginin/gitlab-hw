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


Сотрудники (

   - идентификатор, первичный ключ, serial

   - Last Name (Фамилия сотрудника, varchar(50)

   - First Name (Имя сотрудника, varchar(50)

   - Middle Name (Отчество сотрудника, varchar(50)

   - Оклад, внешний ключ, integer

   - Должность, внешний ключ, integer

   - Тип подразделения, внешний ключ, integer

   - Идентификатор структурного подразделения, внешний ключ, integer

   - Дата найма, date

   - Адрес филиала, внешний ключ, integer

   - Проект на который назначен, внешний ключ, integer


 
Структурные подразделения (

   - идентификатор, первичный ключ, serial

   - Название подразделения, varchar(50)

   - Руководитель подразделения, varchar(100)

   - Описание подразделения, text)

 

Проекты (

   - идентификатор, первичный ключ, serial

   - Название проекта, varchar(100)

   - Дата старта проекта, date

   - Дата завершения проекта, date

   - Руководитель проекта, varchar(100))


 
Филиалы (

   - идентификатор, первичный ключ, serial

   - Название филиала, varchar(50)

   - Город филиала, varchar(50)

   - Штат филиала, varchar(50)

   - Страна филиала, varchar(50))


 
Оклады (

   - идентификатор, первичный ключ, serial

   - Идентификатор сотрудника, внешний ключ, integer

   - Сумма оклада, numeric

   - Дата начисления оклада, date)

 

Должности (

   - идентификатор, первичный ключ, serial

   - Название должности, varchar(50)

   - Обязанности, text

   - Требования к квалификации, text)


 
Назначения (

   - Идентификатор сотрудника, внешний ключ, integer

   - Идентификатор проекта, внешний ключ, integer

   - Дата начала назначения, date

   - Дата завершения назначения, date)


 
Данные типы в PostgreSQL:

- serial - автоинкрементируемое целое число

- varchar(50) - строка переменной длины до 50 символов

- numeric - числовой тип с фиксированной точностью

- integer - целое число

- date - тип даты
