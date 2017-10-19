FROM alpine:3.6

LABEL maintainer=slpcat@qq.com

ENV TERM="xterm" \
    LANG="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8"
TIMEZONE="Europe/Helsinki"

PHP_FPM_USER="www"
PHP_FPM_GROUP="www"
PHP_FPM_LISTEN_MODE="0660"
PHP_MEMORY_LIMIT="512M"
PHP_MAX_UPLOAD="50M"
PHP_MAX_FILE_UPLOAD="200"
PHP_MAX_POST="100M"
PHP_DISPLAY_ERRORS="On"
PHP_DISPLAY_STARTUP_ERRORS="On"
PHP_ERROR_REPORTING="E_COMPILE_ERROR\|E_RECOVERABLE_ERROR\|E_ERROR\|E_CORE_ERROR"
PHP_CGI_FIX_PATHINFO=0


COPY etc /etc/

RUN set -x \
    # Add community
    #&& echo http://dl-4.alpinelinux.org/alpine/v3.6/community/ >> /etc/apk/repositories \
    # System update to latest
    && apk update \
    && apk upgrade \
    # Install base stuff
    && apk add tzdata \
    # Set timezone
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
echo "${TIMEZONE}" > /etc/timezone

    && apk add \
        ca-certificates \
        nginx \
        openssl \
php5 php5-curl php5-fpm php5-gd  php5-mcrypt
php5-opcache
php5-pear
php5-mysql
php5-mysqli
php5-pdo_mysql
php5-openssl
ln -sf /usr/bin/php5 /usr/bin/php
adduser -D -u 1000 -g 'www' www
mkdir /www
chown -R www:www /var/lib/nginx
chown -R www:www /www

#Timezone configuration for php
sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php5/php.ini
#Modifying configuration file php-fpm.conf
sed -i "s|;listen.owner\s*=\s*nobody|listen.owner = ${PHP_FPM_USER}|g" /etc/php5/php-fpm.conf
sed -i "s|;listen.group\s*=\s*nobody|listen.group = ${PHP_FPM_GROUP}|g" /etc/php5/php-fpm.conf
sed -i "s|;listen.mode\s*=\s*0660|listen.mode = ${PHP_FPM_LISTEN_MODE}|g" /etc/php5/php-fpm.conf
sed -i "s|user\s*=\s*nobody|user = ${PHP_FPM_USER}|g" /etc/php5/php-fpm.conf
sed -i "s|group\s*=\s*nobody|group = ${PHP_FPM_GROUP}|g" /etc/php5/php-fpm.conf
sed -i "s|;log_level\s*=\s*notice|log_level = notice|g" /etc/php5/php-fpm.conf #uncommenting line 

#Modifying configuration file php.ini
sed -i "s|display_errors\s*=\s*Off|display_errors = ${PHP_DISPLAY_ERRORS}|i" /etc/php5/php.ini
sed -i "s|display_startup_errors\s*=\s*Off|display_startup_errors = ${PHP_DISPLAY_STARTUP_ERRORS}|i" /etc/php5/php.ini
sed -i "s|error_reporting\s*=\s*E_ALL & ~E_DEPRECATED & ~E_STRICT|error_reporting = ${PHP_ERROR_REPORTING}|i" /etc/php5/php.ini
sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php5/php.ini
sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${PHP_MAX_UPLOAD}|i" /etc/php5/php.ini
sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php5/php.ini
sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php5/php.ini
sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= ${PHP_CGI_FIX_PATHINFO}|i" /etc/php5/php.ini


    # Clean files
    && rm -f /var/cache/apk/*.tar.gz    
