FROM wwek/openresty:alpine

LABEL version="1.0" \
description="openresty alpine" \
maintainer="wwek<licoolgo@gmail.com>"


ARG OPENRESTY_DIR=/usr/local/openresty
ARG OPENRESTY_CONF_DIR=${OPENRESTY_DIR}/nginx/conf

RUN adduser -D -H -u 1000 -s /bin/bash www-data \
    && mkdir -p ${OPENRESTY_CONF_DIR}/conf.d ${OPENRESTY_CONF_DIR}/vhost

ADD nginx.conf ${OPENRESTY_CONF_DIR}
COPY sites/ ${OPENRESTY_CONF_DIR}/sites-available

ARG PHP_UPSTREAM_CONTAINER=php-fpm
ARG PHP_UPSTREAM_PORT=9000

# Set upstream conf and remove the default conf
RUN echo "upstream php-upstream { server ${PHP_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}; }" > ${OPENRESTY_CONF_DIR}/conf.d/upstream.conf 

EXPOSE 80 443

CMD ["/usr/local/openresty/bin/openresty"]
