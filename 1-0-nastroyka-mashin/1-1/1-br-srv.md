---
order: 5
title: 1) BR-SRV
---

auto ens192

iface ens192 inet static

address 192.168.0.2

netmask 255.255.255.240

gateway 192.168.0.1

-  SSH

**adduser sshuser**

**пароль** [P@ssw0rd](mailto:P@ssw0rd)

**usermod -u 2011 sshuser**

**visudo**

**nano /etc/ssh/sshd_config**

Изменяем **Port 2011**

Дописываем **AllowUsers sshuser**

Убираем комментарий у **PermitRootLogin prohibit-password**

Изменяем **MaxAuthTries 2**

Изменяем **Banner /etc/ssh-banner**



Создаём файл /etc/ssh-banner и пишем в него текст **Authorized access only**

**ssh-keygen -t rsa -b 4096 (скипаем всё)**

**ssh-copy-id -p 2011 sshuser@сервер-другой**



/27 = 32

hq-srv(vlan111) /27 | .224 | не более 32 адреса

hq-cli(vlan211) /27 | .224 | не менее 16 адреса

сеть-управ.(vlan811) /29 | .248 | не более 8

br-srv /28 | .240 | не более 16

Занести данные адресов в таблицу приложения для отчёта