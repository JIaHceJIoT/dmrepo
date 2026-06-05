---
order: 1
title: HQ-RTR для DHCP
---

На **HQ-RTR:**

apt-get update && apt install isc-dhcp-server -y

nano /etc/default/isc-dhcp-server

INTERFACESv4=”ens224:1”

nano /etc/dhcp/dhcpd.conf

Комментируем все белые строки

subnet 192.168.211.0 netmask 255.255.255.224 \{

range 192.168.211.2 192.168.211.30;

option domain-name-servers 192.168.111.2;

option routers 192.168.211.1;

option domain-name "au-team.irpo";

default-lease-time 600;

max-lease-time 7200;

}

systemctl restart isc-dhcp-server

Проверяем ip адрес HQ-CLI