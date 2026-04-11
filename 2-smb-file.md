---
order: 10
title: 2 SMB-file
---

HQ-SRV

Устанавливаем утилиту mdadm

apt install mdadm

Выведем список дисков командой lsblk

mdadm --create --verbose /dev/md0 -l 5 -n 3 /dev/sd\{b,c}

Проверим массив, введя снова команду lsblk

Сохраним конфигурацию массива

mdadm --detail --scan | tee /etc/mdadm.conf

update-initramfs -u

Создаём раздел и форматируем его в ext4

mkfs.ext4 /dev/md0

Создаём директорию и монтируем в неё массив

mkdir /raid5

mount /dev/md0 /raid5

Настроим автоматическое монтирование

echo '/dev/md0 /raid5 ext4 defaults 0 0' | tee -a /etc/fstab