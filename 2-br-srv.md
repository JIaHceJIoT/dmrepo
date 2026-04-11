---
order: 9
title: 2 samba BR-SRV
---

BR-SRV

Для начала нужно установить пакеты SAMBA:

apt update && apt install samba\* krb5\*



Переходим в конфигурационный файл: /etc/krb5.conf

\[logging\]

default = FILE: /var/log/krb5libs.log

kdc = FILE: /var/log/krb5kdc.log

admin_server = FILE: /var/log/kadmind.log

\[libdefaults\]

dns_lookup_realm = false

dns_lookup_kdc = true

ticket_lifetime = 24h

forwardable = true

default_realm = true

default_realm = AU-TEAM.IRPO

\[realms\]

AU-TEAM.IRPO = \{

kdc [br-srv.au](http://br-srv.au)\-team.irpo

admin_server = [br-srv.au](http://br-srv.au)\-team.irpo

}

\[domain_realm\]

.au-team.irpo= AU-TEAM.IRPO

au-team.irpo= AU-TEAM.IRPO



Удаляем файл: /etc/samba/smb.conf



samba-tool domain provision --use-rfc2307 --interactive

(Перезапускам и проверяем статус samba

Если в при проверке статуса samba есть какая-то ошибка, то смотрим, есть ли жалоба на какой-то процесс. Выводится id процесса. Убиваем процесс командой kill id\_процесса)

Проверяем работу домена командами

samba-tool domain info 127.0.0.1

samba-tool domain info 192.168.0.2

Создаём пользователей командами

samba-tool user add user1.hq P@ssw0rd

samba-tool user add user2.hq P@ssw0rd

samba-tool user add user3.hq P@ssw0rd

samba-tool user add user4.hq P@ssw0rd

samba-tool user add user5.hq P@ssw0rd

Создаём группу и добавляем туда пользователей:

samba-tool group add hq

samba-tool group addmembers hq user1.hq,user2.hq,user3.hq,user4.hq,user5.hq

Для присоединения машины к домену используется команда

realm join AU-TEAM.IRPO -U Administrator

%hq ALL=(ALL) /usr/bin/cat, /usr/bind/grep, /usr/bind/id

%hq ALL=(ALL) NOPASSWD:/usr/bin/cat, /usr/bind/grep, /usr/bind/id

Заходим в файл /etc/sudoers.d/hq