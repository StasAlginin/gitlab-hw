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

Код и скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy:


sudo apt install haproxy -y

sudo nano /etc/haproxy/haproxy.cfg

Вносим:

listen stats  # веб-страница со статистикой

        bind                    :888

        mode                    http

        stats                   enable

        stats uri               /stats

        stats refresh           5s

        stats realm             Haproxy\ Statistics






frontend example  # секция фронтенд

        mode http

        bind :8088

        #default_backend web_servers

        acl ACL_example.com hdr(host) -i example.com

        use_backend web_servers if ACL_example.com





backend web_servers    # секция бэкенд

        mode http

        balance roundrobin 4

        option httpchk

        http-check send meth GET uri /index.html

        server s1 127.0.0.1:8888 check

        server s2 127.0.0.1:9999 check



listen web_tcp

        bind :1325

        server s1 127.0.0.1:8888 check inter 3s
        server s2 127.0.0.1:9999 check inter 3s


После

sudo systemctl reload haproxy.service

curl http://127.0.0.1:8080


![one](https://github.com/StasAlginin/gitlab-hw/blob/main/img/one.jpeg)

### Задание 2

Код и скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него:


sudo apt install curl

sudo mkdir http1

sudo mkdir http2

sudo mkdir http3

С разных вкладок

cd http1

cd http2

cd http3

И во всех 3х директориях

sudo nano index.html

Вносим

Server 1 Port 8888

Server 1 Port 9999

Server 1 Port 7777

После

sudo nano /etc/nginx/conf.d/example-http.conf

Вносим

include /etc/nginx/include/upstream.inc;





server {

   listen       80;





   server_name  example.local;





   access_log   /var/log/nginx/example-http.com-acess.log;

   error_log    /var/log/nginx/example-http.com-error.log;





   location / {

                proxy_pass      http://example_app;





   }




}


После

sudo nano /etc/nginx/include/upstream.inc

Вносим

upstream example_app {




        server 127.0.0.1:8888 weight=2;

        server 127.0.0.1:9999 weight=3;

        server 127.0.0.1:7777 weight=4;




}


После

sudo nginx -t

sudo systemctl reload nginx.service 

sudo curl -H 'Host: example-http.com' http://localhost


![two](https://github.com/StasAlginin/gitlab-hw/blob/main/img/two.jpeg)

