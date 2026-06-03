---
order: 1
title: "1.1"
---

hostnamectl set-hostname

timedatectl set-timezone Asia/Tomsk

nano /etc/resolv.conf

nameserver 192.168.100.2

nameserver 1.1.1.1 (после настройки DNS удалить строчку)

chattr +i /etc/resolv.conf

nano /etc/sysctl.conf

nano /etc/apt/sources.list



/27 = 32

hq-srv(vlan111) /27 | .224 | не более 32 адреса

hq-cli(vlan211) /27 | .224 | не менее 16 адреса

сеть-управ.(vlan811) /29 | .248 | не более 8

br-srv /28 | .240 | не более 16

Занести данные адресов в таблицу приложения для отчёта