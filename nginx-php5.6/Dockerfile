FROM webdevops/php-nginx:debian-8

LABEL maintainer=slpcat@qq.com

ENV \
    #Container variables
    TERM="xterm" \
    LANG="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    TIMEZONE="Asia/Shanghai" \
    #PHP FPM variables
    PHP_FPM_USER="www" \
    PHP_FPM_GROUP="www" \
    PHP_FPM_LISTEN_MODE="0660"


COPY etc /etc/

RUN set -x \
    # Add repo

    # System update to latest
    && apt-get remove nginx \
    && unlink /etc/nginx/conf.d/10-docker.conf \
    && apt-get update \
    && apt-get dist-upgrade -y \
    # Install base stuff
    # Set timezone
    && ln -sf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone \
    && apt-get install -y \
        nginx \
        ca-certificates \
        php5-xdebug \
        php5-dev \
        autoconf \
        make \
        gcc \
    && ln -sf /usr/bin/php5 /usr/bin/php \
    && pecl install yaf-2.3.5 \
    && echo "extension=yaf.so" > /etc/php5/mods-available/yaf.ini \
    && ln -sf /etc/php5/mods-available/yaf.ini /etc/php5/fpm/conf.d/20-yaf.ini \
    && ln -sf /etc/php5/mods-available/yaf.ini /etc/php5/cli/conf.d/20-yaf.ini \
    # Clean files
    && docker-image-cleanup
