# 使用 Docker 来安装各种应用
[TOC]

### 安装 Drupal CMS
- [offical](https://www.drupal.org/docs/8/api)
- [主题开发](https://www.cnblogs.com/maziang/p/Drupal-Theme-Tutorial.html)
- [模块开发](http://blog.sina.com.cn/s/blog_5a8b8eb80100r8gy.html)
```
docker run --name drupal8 --network kong-net -d \
    -p 11000:80 \
    -v /data/drupal/modules:/var/www/html/modules \
    -v /data/drupal/profiles:/var/www/html/profiles \
    -v /data/drupal/sites:/var/www/html/sites \
    -v /data/drupal/themes:/var/www/html/themes \
    drupal:8.6-fpm-alpine
```

### 安装 WORDPRESS CMS
```
docker run -d --network=kong-net --restart on-failure:5 -p 3306:3306   \
 -v "/data/mysql-data-5.7":"/var/lib/mysql"  -e MYSQL_ROOT_PASSWORD="ALIYUN_123"  --name mysql mysql:5.7    
 mysql:8.0.16

docker run -d --rm \
    --name wordpress \
    --network=kong-net -p 18080:80 \
    -e WORDPRESS_DB_HOST=mysql \
    -e WORDPRESS_DB_USER=root \
    -e WORDPRESS_DB_PASSWORD="ALIYUN_123" \
    -e WORDPRESS_DB_NAME=wordpress \
    -e WORDPRESS_DEBUG=1 \
    -v /data/wordpress-html:/var/www/html \
    wordpress:5.0.3-apache 


docker run -d -p 18080:80 --network=kong-net\
                    -e PMA_HOST=mysql \
                    -e PMA_PORT=3306 \
                    -e PMA_USER=root \
                    -e PMA_PASSWORD=ALIYUN_123 \
                    phpmyadmin/phpmyadmin

docker run --rm --name myadmin -d --network=kong-net --link mysql:mysql -p 28080:80 phpmyadmin/phpmyadmin
```
