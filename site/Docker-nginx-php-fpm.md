# Как мы запустим связку nginx php-fpm через docker
Опишем, как мы будем запускать файл связку nginx php-fpm

```shell
# nginx
docker build --file=site/docker/nginx/Dockerfile --tag=site-nginx site
# php-fpm
docker build --file=site/docker/php-fpm/Dockerfile --tag=site-php-fpm site

```
И что-бы они работали в одной сети нужно создать сеть
```shell
docker network create site
docker run -d --network site --name php-fpm site-php-fpm
docker run -d --network site --name nginx -p 8080:80 site-nginx 
```
Останавливаем так
```shell
docker rm -f php-fpm nginx
docker network rm site
```
