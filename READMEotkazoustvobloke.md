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

sudo apt update

sudo apt upgrade

sudo apt-get install wireguard

sudo mv Stas-ASK.conf /etc/wireguard/

sudo apt-get install resolvconf

sudo wg-quick up Stas-ASK

sudo wg show

curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -

sudo apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"

sudo apt install terraform

(sudo apt full-upgrade; sudo apt autoremove)

sudo mkdir terra

cd terra/

sudo mv terraform /home/algininss/terra/

sudo nano resources.tf


Вносим:

terraform {

  required_providers {

    yandex = {

      source = "yandex-cloud/yandex"

    }

  }


  required_version = ">= 0.13"

}


variable "yandex_cloud_token" {

  type = string

  description = "Данная переменная потребует ввести секретный токен в консоли при запуске terraform plan/apply"

}


provider "yandex" {

  token     = Токен yandex

#var.yandex_cloud_token #секретные данные должны быть в сохранности!! Никогда не выкладывайте токен в публичный доступ.

  cloud_id  = "b1gq378knkis2nt2d5ap"

  folder_id = "b1gea92h9dm0oee5biom"

  zone      = "ru-central1-a"

}


resource "yandex_compute_instance" "vm" {

  count = 2

  name = "vm${count.index}"

  platform_id = "standard-v1"

  boot_disk {

    initialize_params {

      image_id = "fd8mk346omlpmp2rvng7" #ubuntu

      size = 15

    }

  }


  resources {

    core_fraction = 5

    cores  = 2

    memory = 2

  }


  network_interface {

    subnet_id = yandex_vpc_subnet.subnet-1.id

    nat       = true

  }


  metadata = {

    user-data = "${file("./meta.yaml")}"

  }

}


resource "yandex_vpc_network" "network-1" {

  name = "network1"

}


resource "yandex_vpc_subnet" "subnet-1" {

  name           = "subnet1"

  zone           = "ru-central1-a"

  network_id     = yandex_vpc_network.network-1.id

  v4_cidr_blocks = ["192.168.10.0/24"]

}


resource "yandex_lb_target_group" "demo1" {

  name = "demo1"

  target {

    subnet_id = yandex_vpc_subnet.subnet-1.id

    address = yandex_compute_instance.vm[0].network_interface.0.ip_address

  }

  target {

    subnet_id = yandex_vpc_subnet.subnet-1.id

    address = yandex_compute_instance.vm[1].network_interface.0.ip_address

  }

}


resource "yandex_lb_network_load_balancer" "lb1" {

  name = "lb1"

  deletion_protection = "false"

  listener {

    name = "my-lb1"

    port = 80

    external_address_spec {

      ip_version = "ipv4"

    }

  }

  attached_target_group {

    target_group_id = yandex_lb_target_group.demo1.id

    healthcheck {

      name = "http"

      http_options {

        port = 80

        path = "/"

      }

    }

  }

}


После:

sudo ssh-keygen

cat ~/.ssh/id_rsa.pub

Копируем и вносим:

sudo nano meta.yaml


Вносим:

cloud-config

users:

  - name: algininss

    groups: sudo

    shell: /bin/bash

    sudo: ['ALL=(ALL) NOPASSWD:ALL']

    ssh-authorized-keys:

      - ssh-rsa ************** algininss@algininss-VirtualBox


После:

sudo curl -sSL https://storage.yandexcloud.net/yandexcloud-yc/install.sh | bash

sudo yc init

sudo terraform apply

Вносим токен и подтверждаем создание

После подключаемся по SSH к 1 и 2 VM

ssh algininss@****

sudo su

apt update

apt upgrade

apt install nginx

sudo nano /var/www/html/index.nginx-debian.html


Вносим:

<!DOCTYPE html>

<html>

<head>

    <title>VM2</title>

</head>

<body>

    <h1>ITS MY VM2</h1>

</body>

</html>


После:

systemctl restart nginx

exit


![1](https://github.com/StasAlginin/gitlab-hw/blob/main/img/otkazoustvoblake1.png)


![2](https://github.com/StasAlginin/gitlab-hw/blob/main/img/otkazoustvoblake2.png)


![3](https://github.com/StasAlginin/gitlab-hw/blob/main/img/otkazoustvoblake3.png)


![4](https://github.com/StasAlginin/gitlab-hw/blob/main/img/otkazoustvoblake4.png)


![5](https://github.com/StasAlginin/gitlab-hw/blob/main/img/otkazoustvoblake5.png)


Отключаем 1VM


![6](https://github.com/StasAlginin/gitlab-hw/blob/main/img/otkazoustvoblake6.png)


![7](https://github.com/StasAlginin/gitlab-hw/blob/main/img/otkazoustvoblake7.png)
