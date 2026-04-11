---
order: 6
title: BR-SRV
---

auto ens192

iface ens192 inet static

address 192.168.0.2

netmask 255.255.255.240

gateway 192.168.0.1



**adduser sshuser**

**пароль** [P@ssw0rd](mailto:P@ssw0rd)

**usermod -u 2026 sshuser**

**visudo**

**nano /etc/ssh/sshd_config**

Изменяем **Port 2026**

Дописываем **AllowUsers sshuser**

Убираем комментарий у **PermitRootLogin prohibit-password**

Изменяем **MaxAuthTries 2**

Изменяем **Banner /etc/ssh-banner**

Создаём файл /etc/ssh-banner и пишем в него текст **Authorized access only**



**ssh-keygen -t rsa -b 4096 (скипаем всё)**

**ssh-copy-id -p 2026 sshuser@сервер-другой**