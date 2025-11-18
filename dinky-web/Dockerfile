# 使用基础镜像
FROM dinkydocker/dinky-standalone-server:1.2.2-flink1.20
 
# 添加镜像的维护者信息
LABEL maintainer="lushaojun"
 
# 安装 Nginx 和所需软件
RUN apt-get update && apt-get install -y wget nginx locales vim \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN chown root.flink /usr/sbin/nginx && chmod 750 /usr/sbin/nginx && chmod u+s /usr/sbin/nginx && mkdir -p /var/log/nginx && chmod -R 777 /var/log/nginx
 
# 设置中文环境
RUN locale-gen zh_CN.UTF-8
ENV LANG zh_CN.UTF-8
ENV LANGUAGE zh_CN:zh
ENV LC_ALL zh_CN.UTF-8

COPY dist /usr/share/nginx/html/dinky
COPY nginx.conf /etc/nginx/conf.d/default.conf
 
# 暴露容器的 80 端口
EXPOSE 80
EXPOSE 8888
 
WORKDIR /opt/dinky/

# 指定容器启动时执行的命令，让 Nginx 前台运行
CMD ["/bin/bash", "-c", "nginx && ./bin/auto.sh startOnPending"]