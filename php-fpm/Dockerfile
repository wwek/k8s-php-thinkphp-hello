#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#
# To edit the 'php-fpm' base Image, visit its repository on Github
#    https://github.com/wwek/php-fpm
#
# To change its version, see the available Tags on the Docker Hub:
#    https://hub.docker.com/r/wwek/php-fpm/tags/
#
# Note: Base Image name format {image-tag}-{php-version}
#

ARG PHP_VERSION=7.2

FROM wwek/php:${PHP_VERSION}-fpm-alpine


#
#--------------------------------------------------------------------------
# Mandatory Software's Installation
#--------------------------------------------------------------------------
#
# Mandatory Software's such as ("mcrypt", "pdo_mysql", "libssl-dev", ....)
# are installed on the base image 'wwek/php-fpm' image. If you want
# to add more Software's or remove existing one, you need to edit the
# base image (https://github.com/wwek/php-fpm).
#

#
#--------------------------------------------------------------------------
# Optional Software's Installation
#--------------------------------------------------------------------------
#
# Optional Software's will only be installed if you set them to `true`
# in the `docker-compose.yml` before the build.
# Example:
#   - INSTALL_ZIP_ARCHIVE=true
#

###########################################################################
# PHP  EXTENSION
###########################################################################

RUN apk --no-cache add pcre-dev ${PHPIZE_DEPS} libzip-dev \ 
    # Install Php Mysql Client
    &&  docker-php-ext-install mysqli pdo pdo_mysql \
    # Install Php  Extension
    &&  printf "\n" | pecl install redis ZendOpcache zip \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis opcache zip \
    &&  apk del pcre-dev ${PHPIZE_DEPS}


# Copy opcache configration
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini


###########################################################################
# Check PHP version:
###########################################################################

ARG PHP_VERSION=${PHP_VERSION}

RUN php -v | head -n 1 | grep -q "PHP ${PHP_VERSION}."

#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

COPY ./phpext.ini /usr/local/etc/php/conf.d
COPY ./xweb.pool.conf /usr/local/etc/php-fpm.d/

USER root

# Clean up

# 环境变量
ENV MYSQL_HOSTNAME= \
    MYSQL_USERNAME= \
    MYSQL_PASSWORD= 

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
