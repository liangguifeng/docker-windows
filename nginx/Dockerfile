# 采用Nginx的官方镜像
FROM nginx:1.17

#作者信息
MAINTAINER liangguifeng <1476982312@qq.com>

# 环境变量
ENV TZ=Asia/Shanghai

# Nginx的虚拟主机配置
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

#备注信息
LABEL Author="liangguifeng"
LABEL Version="1.0"
LABEL Description="Nginx 1.17 开发环境镜像. "