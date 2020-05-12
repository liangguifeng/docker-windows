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
    && apt-get install -y --no-install-recommends ssh unzip net-tools git wget zsh ssl-cert vim unixodbc-dev libzip-dev libssl-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmagickwand-dev libmcrypt-dev libmemcached-dev zlib1g-dev libpq-dev unixodbc-dev \
    && git config --global user.name "liangguifeng" \
    && git config --global user.email 1476982312@qq.com \
    && sh -c "$(curl -fsSL https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh)" \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) bcmath calendar exif gettext sockets dba mysqli pcntl pdo_mysql pdo_pgsql shmop sysvmsg sysvsem sysvshm iconv zip gd \
    && pecl install mcrypt-1.0.3 redis-5.0.2 xdebug-2.7.2 swoole-4.4.17 \
    && docker-php-ext-enable mcrypt redis xdebug swoole \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install opcache \
    && docker-php-source extract \
    && cd /usr/src/php/ext/odbc \
    && docker-php-source extract \
    && cd /usr/src/php/ext/odbc \
    && phpize \
    && sed -ri 's@^ *test +"\$PHP_.*" *= *"no" *&& *PHP_.*=yes *$@#&@g' configure \
    && ./configure --with-unixODBC=shared,/usr \
    && docker-php-ext-install odbc \
    && docker-php-source delete

# composer安装
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

#备注信息
LABEL Author="liangguifeng"
LABEL Version="1.5"
LABEL Description="PHP 7.3.8 开发环境镜像.自带很多软件，所以包会比较大 "
