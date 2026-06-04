---
order: 9
title: "1.9"
---

Настройка DHCP на HQ-RTR в сторону HQ-CLI

Сведения о настройке занести в отчёт:

1. Настройка конфига (/etc/dhcp/dhcpd.conf)

2. Настройка порта (/etc/default/isc-dhcp-server)

3. Проверка работы службы (systemctl status isc-dhcp-server)

4. Результат выдачи адреса (ip -c a и вывод cat /etc/resolv.conf)