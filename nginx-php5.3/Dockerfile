FROM alpine:3.6

LABEL maintainer=slpcat@qq.com

ENV TERM="xterm" \
    LANG="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    TIME_ZONE="Asia/Shanghai" \


COPY etc /etc/

RUN set -x \
    # Add community
    #&& echo http://dl-4.alpinelinux.org/alpine/v3.6/community/ >> /etc/apk/repositories \
    # System update
    && /usr/local/bin/apk-upgrade \
    # Install base stuff
    && /usr/local/bin/apk-install \
        bash \
        ca-certificates \
        openssl \

    # Set timezone
    #&& echo "${TIME_ZONE}" > /etc/timezone \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && update-ca-certificates 
