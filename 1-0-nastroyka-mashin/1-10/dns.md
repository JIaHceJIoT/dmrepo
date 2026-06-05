---
order: 1
title: HQ-SRV для DNS
---

Настройка на HQ-SRV

apt update && apt install bind9 -y

nano /etc/bind/named.conf.options

В нём добавляем forwarding на 1.1.1.1 или любой другой общедоступный адрес

Под всеми слэшами до закрывающейся скобки пишем:

dnssec-validation no;

allow-query \{ any; };

listen-on-v6 \{ none; };

Далее в nano /etc/bind/named.conf.default-zones

удаляем или комментируем все зоны

, и добавляем свои:

```
zone "au-team.irpo" {
type master;
file "/etc/bind/au-team.db";
};
zone "111.168.192.in-addr.arpa" {
type master;
file "/etc/bind/100.db";
};
zone "211.168.192.in-addr.arpa" {
type master;
file "/etc/bind/200.db";
};
zone "0.168.192.in-addr.arpa" {
type master;
file "/etc/bind/0.db";
};
```

cp /etc/bind/db.empty /etc/bind/au-team.db

cp /etc/bind/db.empty /etc/bind/111.db

cp /etc/bind/db.empty /etc/bind/211.db

cp /etc/bind/db.empty /etc/bind/0.db

nano /etc/bind/au-team.db

В SOA пишем `au-team.irpo. root.au-team.irpo.`

В записи:

```
@ IN NS au-team.irpo.
@ IN A 192.168.111.2
hq-srv IN A 192.168.111.2
hq-cli IN A 192.168.211.2
hq-rtr IN A 192.168.111.1
hq-rtr IN A 192.168.211.1
br-rtr IN A 192.168.0.1
br-srv IN A 192.168.0.2
moodle IN A 192.168.111.2
wiki IN A 192.168.0.2
```

(У мудл и вики можно написать доменное имя за вместо адреса)

/etc/bind/111.db

В SOA пишем `au-team.irpo. root.au-team.irpo.`

В записи:

```
@ IN NS au-team.irpo.
1 IN PTR hq-rtr.au-team.irpo.
2 IN PTR hq-srv.au-team.irpo.
```

/etc/bind/211.db

В SOA пишем `au-team.irpo. root.au-team.irpo.`

В записи:

```
@ IN NS au-team.irpo.
1 IN PTR hq-rtr.au-team.irpo.
2 IN PTR hq-cli.au-team.irpo.
```

/etc/bind/0.db

В SOA пишем `au-team.irpo. root.au-team.irpo.`

В записи:

```
@ IN NS au-team.irpo.
1 IN PTR br-rtr.au-team.irpo.
2 IN PTR br-srv.au-team.irpo.
```

Проверка:

`systemctl restart bind9`

(ОБЯЗАТЕЛЬНО ПЕРЕЗАПУСТИТЬ)

systemctl status bind9

named-checkconf -z

dig (@ip\_сервер) доменное\_имя\_устройства

nslookup доменное\_имя\_устройства

ping -c 2 доменное\_имя\_устройства