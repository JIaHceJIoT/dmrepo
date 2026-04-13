---
order: 5
title: 1) BR-RTR
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

ttl 255



-  Интернет

apt-get update && apt-get install iptables iptables-persistent -y

iptables -t nat -A POSTROUTING -s 192.168.0.0/28 -o ens192 -j MASQUERADE

iptables-save > /etc/iptables/rules.v4



-  SSH

adduser net_admin

visudo

apt install frr -y

nano /etc/frr/daemons

ospfd = yes



-  OSPF (FRR)

systemctl enable frr

systemctl restart frr

vtysh

conf t

ip forwarding

router ospf

passive-interface default

network 192.168.0.0/28 area 0

network 10.10.0.0/30 area 0

area 0 authentication

exit

interface tun1

no ip ospf network broadcast

no ip ospf passive

ip ospf authentication

ip ospf authentication-key P@ssw0rd

exit

do wr