---
order: 16
title: 2.5 Docker
---

На BR-SRV:

```
apt install docker.io docker-compose -y
```

Монтирование cdrom:

```
sudo mount -t iso9660 -o ro /dev/sr0 /mnt/
```

Импорт образов:

```
cd /mnt/docker
docker load -i mariadb_latest.tar
docker load -i site_latest.tar
```

Теперь:

```
mkdir /opt/site
cat > /opt/site/docker-compose.yml <<EOF
services:
  site:
    container_name: site
    image: site:latest
    restart: always
    ports:
      - "8081:8000"
    environment:
      DB_HOST: "192.168.0.2"
      DB_PORT: "3306"
      DB_NAME: testdb1
      DB_USER: test1
      DB_PASS: P@ssw0rd
      DB_TYPE: maria
    depends_on:
      - db

  db:
    container_name: db
    image: mariadb:10.11
    restart: always
    ports:
      - "3306:3306"
    environment:
      MARIADB_USER: test1
      MARIADB_PASSWORD: P@ssw0rd
      MARIADB_DATABASE: testdb1
      MARIADB_ROOT_PASSWORD: P@ssw0rd
         
EOF
cd /opt/site
docker-compose up -d
```