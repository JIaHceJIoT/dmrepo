---
order: 14
title: 2.3 NFS
---

Занести в отчёт:

1) основную настройку hq-srv

2) основное монтирование на hq-cli

3) проверка работы

## **HQ-SRV**

```
apt install nfs-kernel-server -y
```

Далее:

```
mkdir /raid/nfs
chmod 777 /raid/nfs
echo '/raid/nfs 192.168.211.0/27(rw,sync,no_subtree_check)' | tee -a /etc/exports
systemctl restart nfs-kernel-server
```

## **HQ-CLI**

```
apt install nfs-common -y
```

Далее:

```
mkdir /mnt/nfs
echo '192.168.111.2:/raid/nfs /mnt/nfs nfs defaults 0 0' | tee -a /etc/fstab
systemctl daemon-reload
mount -a
```

Проверка:

```
df -h
```