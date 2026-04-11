---
order: 1
title: 1.* (для интернета)
---

Для интернета

apt-get update && apt-get install iptables iptables-persistent -y

На ISP:

-  iptables –t nat –A POSTROUTING –s 172.16.1.0/28 –o ens192 –j MASQUERADE

-  iptables –t nat –A POSTROUTING –s 172.16.2.0/28 –o ens192 –j MASQUERADE

-  iptables-save > /etc/iptables/rules.v4

На HQ:

-  iptables –t nat –A POSTROUTING –s 192.168.100.0/27 –o ens192 –j MASQUERADE

-  iptables –t nat –A POSTROUTING –s 192.168.200.0/27 –o ens192 –j MASQUERADE

-  iptables-save > /etc/iptables/rules.v4

На BR:

-  iptables –t nat –A POSTROUTING –s 192.168.0.0/28 –o ens192 –j MASQUERADE

-  iptables-save > /etc/iptables/rules.v4



<view defs="hierarchy=none" display="List"/>