FROM busybox:latest

# 环境变量
ENV APPROOT="/var/www/k8s-php-thinkphp-hello/" \
    MYSQL_HOSTNAME= \
    MYSQL_USERNAME= \
    MYSQL_PASSWORD= 

# app预处理
RUN mkdir -p $APPROOT

# 配置
WORKDIR $APPROOT

# 安装Thinkphp5.1框架
ARG TP_VERSION=5.1.8
RUN wget -c https://github.com/top-think/framework/archive/v${TP_VERSION}.zip -O tpfw${TP_VERSION}.zip \
    && unzip tpfw${TP_VERSION}.zip && mv framework-${TP_VERSION} thinkphp \
    && wget -c https://github.com/top-think/think/archive/v${TP_VERSION}.zip -O tp${TP_VERSION}.zip \
    && unzip tp${TP_VERSION}.zip && mv think-${TP_VERSION}/* ./

ADD ./phpinfo.php $APPROOT/public 

# 挂载
VOLUME $APPROOT

# 入口
CMD ["sh"]