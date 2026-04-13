---
order: 2
title: 1) ISP
---

nano /etc/network/interfaces

auto ens224

iface ens224 inet static

address 172.16.1.1

netmask 255.255.255.224

auto ens256

iface ens256 inet static

address 172.16.2.1

netmask 255.255.255.240



post-up ip route list | grep -q "192.168.100.0/27 via 172.16.1.2" || ip route add 192.168.100.0/27 via 172.16.1.2 dev ens224

post-up ip route list | grep -q "192.168.0.0/28 via 172.16.2.2" || ip route add 192.168.0.0/28 via 172.16.2.2 dev ens256



apt-get update && apt-get install iptables iptables-persistent -y

iptables –t nat –A POSTROUTING –s 172.16.1.0/28 –o ens192 –j MASQUERADE

iptables –t nat –A POSTROUTING –s 172.16.2.0/28 –o ens192 –j MASQUERADE

iptables-save > /etc/iptables/rules.v4