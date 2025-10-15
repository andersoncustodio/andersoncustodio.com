---
title: Dicas de Imagens Úteis de Container Docker
type: docs
---

## Redis
```sh
docker run -d --restart unless-stopped -p 6379:6379 redis redis-server
```

## Mailhog
```sh
docker run -d --restart unless-stopped -p 1025:1025 -p 8025:8025 mailhog/mailhog:latest
```

## MySQL

{{< tabs items="MySQL 5.7,MariaDB 10.4" >}}

{{< tab >}}
```sh
docker run -d -v mysql57:/var/lib/mysql --name mysql57  -e MYSQL_ROOT_HOST=% -e MYSQL_ALLOW_EMPTY_PASSWORD=yes --restart unless-stopped -p 3306:3306 mysql:5.7
```
{{< /tab >}}

{{< tab >}}
```sh
docker run -d -v mariadb104:/var/lib/mysql --name mariadb104 -e MYSQL_ROOT_HOST=% -e MYSQL_ALLOW_EMPTY_PASSWORD=yes --restart unless-stopped -p 3306:3306 mariadb:10.4
```
{{< /tab >}}

{{< /tabs >}}

## Elasticserach

{{< tabs items="Elasticserach 7,Elasticserach 6" >}}

{{< tab >}}
```sh
docker run -d --restart unless-stopped --name elasticsearch7 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e "ES_JAVA_OPTS=-Xms1G -Xmx1G" elasticsearch:7.13.2
```
{{< /tab >}}

{{< tab >}}
```sh
docker run -d --restart unless-stopped --name elasticsearch6 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e "ES_JAVA_OPTS=-Xms1G -Xmx1G" elasticsearch:6.8.16
```
{{< /tab >}}

{{< /tabs >}}

## SSH Server

```sh
docker run -d \
    --name=openssh-server \
    -e PUID=1000 \
    -e PGID=1000 \
    -e TZ=America/Sao_Paulo \
    -e PASSWORD_ACCESS=true \
    -e USER_PASSWORD=password \
    -e USER_NAME=username \
    -p 2222:2222 \
    -v /path/to/appdata/config:/config \
    --restart unless-stopped \
    ghcr.io/linuxserver/openssh-server
```
