# 来自官方的PHP镜像版本为php:7.3-fpm
FROM php:7.3-fpm

#作者信息
MAINTAINER liangguifeng <1476982312@qq.com>

# 设置环境变量
ENV TZ=Asia/Shanghai

# 换源以及安装扩展等等
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak \
    && echo 'deb http://mirrors.aliyun.com/debian/ buster main non-free contrib' > /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/debian-security buster/updates main' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib' >> /etc/apt/sources.list \
    && apt-get update \
    && export CFLAGS="$PHP_CFLAGS" CPPFLAGS="$PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS" \
    && apt-get install -y --no-install-recommends vim libssl-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmagickwand-dev libmcrypt-dev libmemcached-dev zlib1g-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) bcmath calendar exif gettext sockets dba mysqli pcntl pdo_mysql shmop sysvmsg sysvsem sysvshm iconv gd \
    && pecl install mcrypt-1.0.3 redis-5.0.2 xdebug-2.7.2 swoole-4.4.17 \
    && docker-php-ext-enable mcrypt redis xdebug swoole \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install opcache

# composer安装失败，只能自己来了
# 跑这个一遍跑完:
# curl -sS https://getcomposer.org/installer -o composer-setup.php
# php composer-setup.php --install-dir=/usr/local/bin --filename=composer
#RUN curl -sS https://getcomposer.org/installer | php \
#    && chmod a+x composer.phar \
#    && mv composer.phar /usr/local/bin/composer \
#    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
#    && composer global require "laravel/installer"

#备注信息
LABEL Author="liangguifeng"
LABEL Version="1.0"
LABEL Description="PHP 7.3.8 开发环境镜像. "
