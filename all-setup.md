---
order: 1.5
title: All setup
---

hostnamectl set-hostname

timedatectl set-timezone Asia/Tomsk

nano /etc/resolv.conf

nameserver 192.168.100.2

nameserver 1.1.1.1



chattr +i /etc/resolv.conf

nano /etc/sysctl.conf

nano /etc/apt/sources.list