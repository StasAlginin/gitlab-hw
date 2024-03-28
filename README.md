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

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`

[Ссылка на коммит](https://github.com/StasAlginin/myrepo/commit/a3bec7f8e71fc452c7bc92342ee7f8eb2a18c5da)

Поле для вставки кода...

sudo mkdir myrepo
cd myrepo/
sudo git clone https://github.com/StasAlginin/myrepo.git
sudo git config --global user.name "StasAlginin"
sudo git config --global user.email ass@cyberlab23.ru
sudo git init

git status
Текущая ветка: master
Еще нет коммитов

Неотслеживаемые файлы:
  (используйте «git add <файл>...», чтобы добавить в то, что будет включено в коммит)
	myrepo/

индекс пуст, но есть неотслеживаемые файлы
(используйте «git add», чтобы проиндексировать их)

sudo nano README.md 
#1 vhod

sudo git status 
Текущая ветка: main
Эта ветка соответствует «origin/main».

Изменения, которые не в индексе для коммита:
  (используйте «git add <файл>...», чтобы добавить файл в индекс)
  (используйте «git restore <файл>...», чтобы отменить изменения в рабочем каталоге)
	изменено:      README.md

индекс пуст (используйте «git add» и/или «git commit -a»)

sudo git diff README.md
diff --git a/README.md b/README.md
index 765cd62..876a860 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,3 @@
-# myrepo
\ No newline at end of file
+# myrepo
+
+#1 vhod

sudo git diff --staged README.md

sudo git status 
Текущая ветка: main
Эта ветка соответствует «origin/main».

Изменения, которые не в индексе для коммита:
  (используйте «git add <файл>...», чтобы добавить файл в индекс)
  (используйте «git restore <файл>...», чтобы отменить изменения в рабочем каталоге)
	изменено:      README.md

индекс пуст (используйте «git add» и/или «git commit -a»)

sudo git add README.md
sudo git status 

Текущая ветка: main
Эта ветка соответствует «origin/main».

Изменения, которые будут включены в коммит:
  (используйте «git restore --staged <файл>...», чтобы убрать из индекса)
	изменено:      README.md

sudo git diff README.md

sudo git diff --staged README.md
diff --git a/README.md b/README.md
index 765cd62..876a860 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,3 @@
-# myrepo
\ No newline at end of file
+# myrepo
+
+#1 vhod

sudo git commit -m 'First commit'
[main a3bec7f] First commit
 1 file changed, 3 insertions(+), 1 deletion(-)

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 1](ссылка на скриншот 1)`


### Задание 2

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`

[Ссылка на коммит](https://github.com/StasAlginin/myrepo/commit/d7295860eb4d677e7ad29386a0fc6e846badb02d)

sudo touch .gitignore
sudo nano .gitignore
   *.pyc
   cache/

sudo git status
### Задание 2
Текущая ветка: main
Эта ветка соответствует «origin/main».

Неотслеживаемые файлы:
  (используйте «git add <файл>...», чтобы добавить в то, что будет включено в коммит)
	.gitignore

индекс пуст, но есть неотслеживаемые файлы
(используйте «git add», чтобы проиндексировать их)

sudo git add .gitignore

sudo git status
Текущая ветка: main
Эта ветка соответствует «origin/main».

Изменения, которые будут включены в коммит:
  (используйте «git restore --staged <файл>...», чтобы убрать из индекса)
	новый файл:    .gitignore

sudo git commit -m "Added .gitignore file to ignore .pyc files and cache directory"
[main d729586] Added .gitignore file to ignore .pyc files and cache directory
 1 file changed, 2 insertions(+)
 create mode 100644 .gitignore

sudo git push origin main
Перечисление объектов: 4, готово.
Подсчет объектов: 100% (4/4), готово.
При сжатии изменений используется до 2 потоков
Сжатие объектов: 100% (2/2), готово.
Запись объектов: 100% (3/3), 323 байта | 323.00 КиБ/с, готово.
Всего 3 (изменений 0), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
To https://github.com/StasAlginin/myrepo.git
   9fdc922..d729586  main -> main

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`

[Мой график](https://github.com/StasAlginin/myrepo/network)

sudo git checkout -b dev
Переключились на новую ветку «dev»

sudo nano test.sh 
"This is a test file"

sudo git add test.sh
sudo git status
Текущая ветка: dev
Изменения, которые будут включены в коммит:

  (используйте «git restore --staged <файл>...», чтобы убрать из индекса)
	новый файл:    test.sh

sudo git commit -m "Added test.sh file"
[dev 3cd300f] Added test.sh file
 1 file changed, 1 insertion(+)
 create mode 100644 test.sh

git push origin dev 
fatal: detected dubious ownership in repository at '/home/algininss/myrepo/myrepo'
To add an exception for this directory, call:

	git config --global --add safe.directory /home/algininss/myrepo/myrepo

git config --global --add safe.directory /home/algininss/myrepo/myrepo

git push origin dev 
Username for 'https://github.com': StasAlginin
Password for 'https://StasAlginin@github.com': 
Перечисление объектов: 4, готово.
Подсчет объектов: 100% (4/4), готово.
При сжатии изменений используется до 2 потоков
Сжатие объектов: 100% (2/2), готово.
Запись объектов: 100% (3/3), 334 байта | 334.00 КиБ/с, готово.
Всего 3 (изменений 0), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: 
remote: Create a pull request for 'dev' on GitHub by visiting:
remote:      https://github.com/StasAlginin/myrepo/pull/new/dev
remote: 
To https://github.com/StasAlginin/myrepo.git
 * [new branch]      dev -> dev
error: update_ref failed for ref 'refs/remotes/origin/dev': cannot lock ref 'refs/remotes/origin/dev': Не удалось создать «/home/algininss/myrepo/myrepo/.git/refs/remotes/origin/dev.lock»: Отказано в доступе

sudo git push origin dev 
Everything up-to-date

sudo git checkout main
Переключились на ветку «main»
Эта ветка соответствует «origin/main».

sudo nano main.sh
"This is the main file"

sudo git add main.sh

sudo git commit -m "Added main.sh file"
[main a155382] Added main.sh file
 1 file changed, 1 insertion(+)
 create mode 100644 main.sh

 sudo git push origin main
Перечисление объектов: 4, готово.
Подсчет объектов: 100% (4/4), готово.
При сжатии изменений используется до 2 потоков
Сжатие объектов: 100% (2/2), готово.
Запись объектов: 100% (3/3), 336 байтов | 336.00 КиБ/с, готово.
Всего 3 (изменений 0), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
To https://github.com/StasAlginin/myrepo.git
   9b3ee52..a155382  main -> main

sudo git merge dev
Merge made by the 'ort' strategy.
 test.sh | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 test.sh

sudo git log
commit bb9ea3a0276cc56c7511657dd559d463b5906e05 (HEAD -> main)
Merge: a155382 3cd300f

Author: StasAlginin <ass@cyberlab23.ru>
Date:   Thu Mar 28 12:34:04 2024 +0300

    Merge branch 'dev'
    information fusion

commit a155382d29d103aa5423be44b58b98d31423e95f (origin/main, origin/HEAD)

Author: StasAlginin <ass@cyberlab23.ru>
Date:   Thu Mar 28 12:33:15 2024 +0300

    Added main.sh file

commit 3cd300f114045a02ba763543b039dfb1d32608b8 (origin/dev, dev)
Author: StasAlginin <ass@cyberlab23.ru>
Date:   Thu Mar 28 12:21:30 2024 +0300

    Added test.sh file

commit 9b3ee52d3aa13257f6a91a9833842b79c9c03502
Author: StasAlginin <ass@cyberlab23.ru>
Date:   Thu Mar 28 12:09:21 2024 +0300

    3 commit

commit d7295860eb4d677e7ad29386a0fc6e846badb02d
Author: StasAlginin <ass@cyberlab23.ru>
Date:   Thu Mar 28 12:06:40 2024 +0300

    Added .gitignore file to ignore .pyc files and cache directory

commit 9fdc92207d7ef13338a947a48df88c3dc7cf7ce3
Author: StasAlginin <ass@cyberlab23.ru>
Date:   Thu Mar 28 12:02:22 2024 +0300

    2 commit

commit a3bec7f8e71fc452c7bc92342ee7f8eb2a18c5da
Author: StasAlginin <ass@cyberlab23.ru>
Date:   Thu Mar 28 10:37:16 2024 +0300

    First commit

commit 288f7411d7519800114380db26c60dd78d31d01b
Author: StasAlginin <164986584+StasAlginin@users.noreply.github.com>
Date:   Thu Mar 28 10:11:47 2024 +0300

    Initial commit

sudo git push origin main
Перечисление объектов: 4, готово.
Подсчет объектов: 100% (4/4), готово.
При сжатии изменений используется до 2 потоков
Сжатие объектов: 100% (2/2), готово.
Запись объектов: 100% (2/2), 308 байтов | 308.00 КиБ/с, готово.
Всего 2 (изменений 1), повторно использовано 0 (изменений 0), повторно использовано пакетов 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/StasAlginin/myrepo.git
   a155382..bb9ea3a  main -> main
