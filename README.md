# docker-windows
[![star](https://gitee.com/liangguifeng/docker-windows/badge/star.svg?theme=dark)](https://gitee.com/liangguifeng/docker-windows/stargazers)
[![Fork me on Gitee](https://gitee.com/liangguifeng/docker-windows/widgets/widget_6.svg)](https://gitee.com/liangguifeng/docker-windows)

#### 介绍
`docker-windows` 这个项目是使用docker-compose进行编排容器的文件，基于 `Windows` 下 `docker` 环境编排

#### 安装教程
- !!! 注意:需要使用该项目，需要预先安装好 `Git`, `Docker for Windows`。

1、 进入系统 `D` 盘根目录

- 如果不想更改 `docker-compose.yml` 文件的话，在 `D` 盘的根目录下克隆项目会更便捷

2、  拉取当前项目代码，并且重命名为 `docker-compose`
```shell script
git clone https://gitee.com/liangguifeng/docker-windows.git docker-compose
```

3、 鼠标右键点击 `Git Bash Here`，输入以下命令
```shell script
#拉取所需镜像
docker pull nginx:1.17
docker pull php:7.3-fpm
docker pull mysql:5.7
docker pull redis:latest
```

```shell script
#构建我们自己的php镜像
cd docker-compose/php
```

```shell script
#打开Dockerfile文件
vim Dockerfile
```

```shell script
#修改第19-20行，更改为自己的git配置
&& git config --global user.name "you username" \
&& git config --global user.email you email \
```

```shell script
#注意下面构建不要忽略所有的“.”号
#为什么我不写到docker-compose的编排文件中是因为不能每次启动都build一下吧，这样太耗时了
docker build -f ./Dockerfile -t php7.3:1.5 .
```

```shell script
#构建成功后，查看所有镜像
docker images
```

```shell script
#此处应该有以下5个镜像，如果不够，请自己排查
· php7.3:1.4
· php:7.3-fpm
· nginx:1.17
· mysql:5.7
· redis:latest
```

```shell script
#回到我们项目的根目录
cd /d/docker-compose
```

```shell script
#然后使用docker-compose来构建我们的容器
docker-compose up -d
```

```shell script
#运行成功可以使用容器id或者容器名称进去容器内
#请Windows上的朋友按照我这个写法进入容器，很多坑我已经踩过了，没必要每个人来都掉下去
winpty docker exec -it php zsh
```


#### 使用说明

1. `docker-windows` 这个项目其实就相当于常规的 `lnmp` + `redis` 环境吧，只不过是在 `docker` 下运行的
我看好多教程都是不太完整，要么就是直接给代码让你去抄，太没意思了，我找了很多文章，都没有理解到
 `docker-compose` 的意义，后面根据自己的理解和猜测，算是明白了 `docker-compose` 的作用，
也写了这个 `demo` 便于许多朋友在 `Windows` 机器上搭建 `PHP` 环境，如果有不明白的地方欢迎共同探讨！

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request

#### 关于作者
1.  个人邮箱：1476982312@qq.com
2.  个人博客：[犯二青年博客](https://findcat.cn)
3.  GitHub：[犯二青年](https://github.com/liangguifeng)