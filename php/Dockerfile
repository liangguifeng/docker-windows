### 来自官方的PHP镜像版本为php:7.3-fpm
### 该版本只包含FPM不包括CLI,所以这里并不能执行composer
### 如果需要用PHP-CLI 需要再开一个CLI容器，或者安装同时包含FPM和CLI的版本
FROM php:7.3-fpm

MAINTAINER liangguifeng <1476982312@qq.com>

### 设置环境变量
ENV TZ=Asia/Shanghai

### 执行bash命令安装php所需的扩展
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
    ### 这里是docker提供的安装php扩展的方法，在这里安装了pdo_mysql扩展还有GD库等
    && docker-php-ext-install iconv bcmath mysqli pdo_mysql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd
