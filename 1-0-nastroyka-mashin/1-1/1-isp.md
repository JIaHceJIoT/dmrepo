---
order: 1
title: 1) ISP
---

nano /etc/network/interfaces

```
auto ens224
iface ens224 inet static
address 172.16.10.1
netmask 255.255.255.240
auto ens256
iface ens256 inet static
address 172.16.20.1
netmask 255.255.255.240
```



Если ospf не захочет работать

```
post-up ip route list | grep -q "192.168.111.0/27 via 172.16.10.2" || ip route add 192.168.100.0/27 via 172.16.1.2 dev ens224 &&
post-up ip route list | grep -q "192.168.0.0/28 via 172.16.20.2" || ip route add 192.168.0.0/28 via 172.16.2.2 dev ens256
```



Интернет

```
apt-get update && apt-get install iptables iptables-persistent -y &&
iptables -t nat -A POSTROUTING -s 172.16.10.0/28 -o ens192 -j MASQUERADE &&
iptables -t nat -A POSTROUTING -s 172.16.20.0/28 -o ens192 -j MASQUERADE &&
iptables-save > /etc/iptables/rules.v4
```



/27 = 32

hq-srv(vlan111) /27 | .224 | не более 32 адреса

hq-cli(vlan211) /27 | .224 | не менее 16 адреса

сеть-управ.(vlan811) /29 | .248 | не более 8

br-srv /28 | .240 | не более 16

Занести данные адресов в таблицу приложения для отчёта