---
order: 13
title: 2.2 RAID
---

Без отчёта

На HQ-SRV:

```
apt install mdadm -y
```

Собрать массив:

```
mdadm --create --verbose /dev/md1 -l 1 -n 2 /dev/sd{b,c}
mdadm --detail --scan | tee /etc/mdadm.conf
update-initramfs -u
```

Форматирование раздела в ext4:

```
mkfs.ext4 /dev/md1
```

Автомонтирование:

```
mkdir /raid
mount /dev/md1 /raid
echo /dev/md1 /raid ext4 defaults 0 0 | tee -a /etc/fstab
```