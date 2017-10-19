FROM webdevops/php-apache:ubuntu-12.04

LABEL maintainer=slpcat@qq.com

ENV \
    #Container variables
    TERM="xterm" \
    LANG="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    TIMEZONE="Asia/Shanghai" \
    APPLICATION_USER="application" \
    APPLICATION_GROUP="application" \
    APPLICATION_PATH="/app" 

COPY www_root /app

RUN set -x \
    # System update to latest
    && apt-get update \
    && apt-get upgrade -y \
    # Install base stuff
    # Set timezone
    && ln -sf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone \
    && chown -R ${APPLICATION_USER}:${APPLICATION_GROUP} ${APPLICATION_PATH} \
    # Clean files
    && docker-image-cleanup
