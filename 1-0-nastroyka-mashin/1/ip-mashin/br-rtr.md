---
order: 4
title: BR-RTR
---

auto ens192

iface ens192 inet static

address 172.16.2.2

netmask 255.255.255.240

gateway 172.16.2.1

auto ens224

iface ens224 inet static

address 192.168.0.1

netmask 255.255.255.240

auto tun1

iface tun1 inet tunnel

address 10.10.0.2

netmask 255.255.255.252

mode gre

local 172.16.2.2

endpoint 172.16.1.2