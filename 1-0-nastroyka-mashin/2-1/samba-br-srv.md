---
order: 1
title: BR-SRV Samba
---

## **BR-SRV**

Сначала:

```
apt install samba winbind -y
```

Затем:

```
rm -rf /etc/samba/smb.conf
samba-tool domain provision --use-rfc2307 --interactive
```

Теперь:

```
systemctl disable --now smbd winbind
systemctl mask smbd winbind
systemctl start samba
```

Группа и 5 пользователей:

```
samba-tool group create hq
for i in {1..5}; do
samba-tool user create hquser$i "P@ssw0rd"
samba-tool group addmembers hq hquser$i
done
```

## **HQ-CLI**

```
apt install krb5-user -y
```

В качестве управляющего сервера необходимо добавить [`br-srv.au`](http://br-srv.au)`-team.irpo`.

Далее:

```
realm join -U Administrator br-srv
```

Теперь надо получить билет:

```
kinit -k 'HQ-CLI$@AU-TEAM.IRPO'
```

Далее для группы прописывается правило:

```
gid=$(getent group hq@au-team.irpo | awk -F: '{print $3}')
echo "%#${gid} ALL=(ALL) /usr/bin/cat, /usr/bin/grep, /usr/bin/id" > /etc/sudoers.d/hq
chmod 440 /etc/sudoers.d/hq
visudo -c
```

Обязательно попробовать войти под пользователем:

```
sudo pam-auth-update --enable mkhomedir
su - hquser1@au-team.irpo
```

## **Troubleshooting**

Если пишет `su: Системная ошибка`:

1. Необходимо сделать на BR-SRV:

```
samba-tool ntacl sysvolreset
```

Попробовать снова переключить пользователя.

1. Попробовать подключиться через smbclient напрямую для просмотра политик:

```
apt install smbclient -y
```

```
smbclient //br-srv/sysvol -k -c 'ls au-team.irpo/Policies'
```

Если ничего не выдало, попробовать:

```
kdestroy
kinit -k 'HQ-CLI$@AU-TEAM.IRPO'
```

И посмотреть тикет, в нем должны быть доменные правила:

```
klist -k /etc/krb5.keytab
```

Попробовать снова `smbclient`. Если получается - сделать первый шаг.

1. Если вообще ничего не выходит - перейти в файл `/etc/sssd/sssd.conf` и добавить следующую строку:

```
ad_gpo_access_mode = disabled
```

Это отключит проверку групповых политик, поэтому должно пустить.