---
order: 11
title: 2) NFS
---

HQ-SRV

Устанавливаем nfs-kernel-server

apt install nfs-kernel-server

mkdir /raid5/nfs

chmod 777 /raid5/nfs

Настроим экспорт массива

echo '/raid5/nfs 192.168.200.0/27(rw,sync,no_subtree_check)' | tee -a /etc/exports



HQ-CLI

Устанавливаем nfs клиент

**apt update && apt install nfs-common**

Создаём директорию для монтирования

**mkdir /mnt/nfs**

Настроим автоматическое монтирование

echo '192.168.100.2:/raid5/nfs /mnt/nfs nfs defaults 0 0' | tee -a /etc/fstab

systemctl daemon-reload

Монтируем

mount -a

Проверяем

df -h

Должна быть строчка с примонтированной директорией.