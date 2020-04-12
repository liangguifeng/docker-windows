# docker-windows

#### 介绍
docker-windows这个项目是使用docker-compose进行编排容器的文件，基于Windows下docker环境编排

#### 安装教程
- !!! 注意:需要使用该项目，需要预先安装好Git, Docker for Windows。

1、 进入系统D盘根目录

- 如果不想更改docker-compose.yml文件的话，在D盘的根目录下克隆项目会更便捷

2、  拉取当前项目代码，并且重命名为docker-compose
```shell script
git clone https://gitee.com/liangguifeng/docker-windows.git docker-compose
```

3、 鼠标右键点击Git Bash Here，输入以下命令
```shell script
#拉取所需镜像
docker pull nginx:1.17
docker pull php:7.3-fpm
docker pull mysql:5.7

#构建我们自己的php镜像
cd docker-compose/php
#注意下面构建不要忽略所有的“.”号
docker build -f ./Dockerfile -t php7.3:1.4 .

#构建成功后，查看所有镜像
docker images

#此处应该有以下4个镜像，如果不够，请自己排查
· php7.3:1.4
· php:7.3-fpm
· nginx:1.17
· mysql:5.7

#回到我们项目的根目录
cd /d/docker-compose

#然后使用docker-compose来构建我们的容器
docker-compose up -d

#运行成功可以使用容器id或者容器名称进去容器内
#请Windows上的朋友按照我这个写法进入容器，很多坑我已经踩过了，没必要每个人来都掉下去
winpty docker exec -it docker-compose_php7.3_1 bash
```


#### 使用说明

1. docker-windows这个项目其实就相当于常规的lnmp环境吧，只不过是在docker下运行的
我看好多教程都是不太完整，要么就是直接给代码让你去抄，太没意思了，我找了很多文章，都没有理解到
docker-compose的意义，后面根据自己的理解和猜测，算是明白了docker-compose的作用，
也写了这个demo便于许多朋友在Windows机器上搭建PHP环境，如果有不明白的地方欢迎共同探讨！

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request

#### 关于作者
1.  邮箱：1476982312@qq.com
2.  博客：[犯二青年博客](https://findcat.cn)