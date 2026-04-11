---
order: 3
title: HQ-RTR
---

auto ens192

iface ens192 inet static

address 172.16.1.2

netmask 255.255.255.240

gateway 172.16.1.1

auto ens224

iface ens224 inet static

address 192.168.100.1

netmask 255.255.255.224

auto ens224:1

iface ens224:1 inet static

address 192.168.200.1

netmask 255.255.255.224

auto ens224:2

iface ens224:2 inet static

address 192.168.99.99

netmask 255.255.255.248

auto ens224.100

iface ens224.100 inet manual

vlan-raw-device ens224

auto ens224.200

iface ens224.200 inet manual

vlan-raw-device ens224:1

auto ens224.999

iface ens224.999 inet manual

vlan-raw-device ens224:2

allow-hotplug tun1

auto tun1

iface tun1 inet tunnel

address 10.10.0.1

netmask 255.255.255.252

mode gre

local 172.16.1.2

endpoint 172.16.2.2

ttl 255



apt-get update && apt-get install iptables iptables-persistent -y

iptables -t nat -A POSTROUTING -s 192.168.100.0/27 -o ens192 -j MASQUERADE

iptables -t nat -A POSTROUTING -s 192.168.200.0/27 -o ens192 -j MASQUERADE

iptables-save > /etc/iptables/rules.v4



adduser -m net_admin

**visudo**

apt install frr -y

nano /etc/frr/daemons

ospfd = yes

systemctl enable frr

**systemctl restart frr**

**vtysh**

**conf t**

**ip forwarding**

**router ospf**

**passive-interface default**

**network 192.168.100.0/27 area 0**

**network 192.168.200.0/27 area 0**

**network 10.10.0.0/30 area 0**

**area 0 authentication**

**exit**

**interface tun1**

**no ip ospf network broadcast**

**no ip ospf passive**

**ip ospf authentication**

**ip ospf authentication-key P@ssw0rd**

**exit**

**do wr**



apt-get update && apt install isc-dhcp-server -y

nano /etc/default/isc-dhcp-server

INTERFACESv4=”ens224:1”

nano /etc/dhcp/dhcpd.conf

Комментируем все белые строки

subnet 192.168.200.0 netmask 255.255.255.224 \{

range 192.168.200.2 192.168.200.4;

option domain-name-servers 192.168.100.2;

option routers 192.168.200.1;

option domain-name "au-team.irpo";

default-lease-time 600;

max-lease-time 7200;

}



systemctl restart isc-dhcp-server

Проверяем ip клиента