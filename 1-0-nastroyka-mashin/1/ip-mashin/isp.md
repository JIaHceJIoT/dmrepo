---
order: 1
title: ISP
---

auto ens224

iface ens224 inet static

address 172.16.1.1

netmask 255.255.255.224

auto ens256

iface ens256 inet static

address 172.16.2.1

netmask 255.255.255.240



Настройка маршрутизации:

post-up ip route list | grep -q "192.168.100.0/27 via 172.16.1.2" || ip route add 192.168.100.0/27 via 172.16.1.2 dev ens224 post-up ip route list | grep -q "192.168.0.0/28 via 172.16.2.2" || ip route add 192.168.0.0/28 via 172.16.2.2 dev ens256