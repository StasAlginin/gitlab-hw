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

Cкриншот, c маршрутизатора:

![cisco](https://github.com/StasAlginin/gitlab-hw/blob/main/img/cisco.jpeg)

### Задание 2


sudo apt update 

sudo apt upgrade

sudo apt install curl -y

sudo ufw enable

sudo ufw allow http

sudo ufw allow 80

sudo ufw allow https

sudo ufw allow 443

sudo ufw allow ftp

sudo ufw allow from 172.16.17.148

sudo ufw status 

sudo apt install nginx

sudo nano /var/www/html/index.nginx-debian.html

На 1 VM вносим в файл:


<!DOCTYPE html>

<html>

<head>

    <title>VM1</title>

</head>

<body>

    <h1>ITS MY VM1</h1>

</body>

</html>


И так же:


sudo nano /var/www/html/scriptchek.sh

Вносим в файл:


#!/bin/bash  

curl 172.16.17.147:80 || exit 1 

[[ -f index.nginx-debian.html ]] || exit 1


После:

sudo systemctl restart nginx.service 

sudo apt install keepalived

sudo nano /etc/keepalived/keepalived.conf

Вносим в файл:



vrrp_script chk_myscript {

       script       "/var/www/html/scriptchek.sh"

       interval 3

       weight 2

}





vrrp_instance VI_1 {

        state MASTER

        interface enp0s3

        virtual_router_id 235

        priority 255

        advert_int 1





        virtual_ipaddress {

              172.16.17.235/24

        }

        track_script {

                   chk_myscript

        }

}

После:

sudo systemctl start keepalived.service 

sudo systemctl status keepalived.service 

sudo ufw allow from 172.16.17.235 (Виртуальный IP)





Настройка 2 виртуальной машины отличается лишь:


sudo ufw allow from 172.16.17.147 вместо 148

sudo nano /var/www/html/index.nginx-debian.html



Вносим в файл:


<!DOCTYPE html>

<html>

<head>

    <title>VM2</title>

</head>

<body>

    <h1>ITS MY VM2</h1>

</body>

</html>




И так же:

sudo nano /etc/keepalived/keepalived.conf


Вносим в файл:


rrp_script chk_myscript {

       script       "/var/www/html/scriptchek.sh"

       interval 3

       weight 2

}




vrrp_instance VI_1 {

        state BACKUP

        interface enp0s3

        virtual_router_id 235

        priority 200

        advert_int 1





        virtual_ipaddress {

              172.16.17.235/24

        }

        track_script {

                   chk_myscript

        }



}


Скриншоты 1 VM когда keepalived MASTER является 1VM


![1VM1](https://github.com/StasAlginin/gitlab-hw/blob/main/img/1VM_its_my_vm1.jpeg)

И так же переходим по виртуальному IP адресу на 2 VM:

![1VM2](https://github.com/StasAlginin/gitlab-hw/blob/main/img/1VM_its_my_vm2.jpeg)


После отключаем nginx на 1 VM

Скриншоты с 1 VM:

![1VM2](https://github.com/StasAlginin/gitlab-hw/blob/main/img/2VM_its_my_vm1.jpeg)


И так же переходим по виртуальному IP адресу на 2 VM:

![2VM2](https://github.com/StasAlginin/gitlab-hw/blob/main/img/2VM_its_my_vm2.jpeg)
