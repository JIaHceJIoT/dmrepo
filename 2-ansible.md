---
order: 13
title: 2) ansible
---

BR-SRV

apt install ansible

ssh-keygen -t rsa

ssh-copy-id -p 2026 sshuser@192.168.100.2

**Тоже самое нужно сделать для остальных машин (cli, br/hq-rtr)**

**mkdir /etc/ansible**

**nano /etc/ansible/hosts**

\[hq\]

192\.168.100.2 ansible_port=2026 ansible_user=sshuser

192\.168.200.2 ansible_port=2026 ansible_user=sshuser

192\.168.100.1 ansible_port=2026 ansible_user=net_admin

\[br\]

192\.168.0.1 ansible_port=2026 ansible_user=net_admin

Для проверки файла инвентаря используется команда ansible all -m ping



Для RTR сначала настроить sshd_config