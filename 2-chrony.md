---
order: 12
title: 2) chrony
---

 

HQ-RTR

apt update && apt install chrony

 systemcl restart chronyd

Теперь на каждую машину, кроме ISP устанавливаем chrony:

apt install chrony

и в файле конфигурации указать сервер hq-rtr (nameserver 192.168.100.1)

перезапускаем chrony: systemctl restart chrony

Проверяем работу командой сhronyc sources