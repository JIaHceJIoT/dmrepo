---
order: 1
title: Базовая настройка машин
---

hostnamectl set-hostname

timedatectl set-timezone Asia/Tomsk

nano /etc/resolv.conf

1\.1.1.1 + 192.168.100.2

chattr +i /etc/resolv.conf

nano /etc/sysctl.conf

nano /etc/apt/sources.list