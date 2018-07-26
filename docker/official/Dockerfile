FROM debian:latest

LABEL maintainer="Darian Raymond <admin@v2ray.com>"

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}

COPY config.json /etc/v2ray/config.json

RUN apt-get update &&DEBIAN_FRONTEND=noninteractive apt-get install -y wget curl apt-utils tzdata tar unzip daemon openssl curl sed net-tools vim \
    && mkdir -p \
    ${V2RAY_LOG_DIR} \
    ${V2RAY_CONFIG_DIR} \
    /tmp/v2ray \
    /var/log/v2ray/ \
    && curl -L -s https://raw.githubusercontent.com/v2ray/v2ray-core/master/release/install-release.sh | bash \
    && mv /etc/v2ray/config.json /etc/v2ray/config.json.bak \
    && chmod +x /etc/v2ray/config.json \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && rm -rf /tmp/v2ray /var/cache/*

ENV PATH /usr/bin/v2ray/v2ray:$PATH

CMD ["v2ray", "-config=/etc/v2ray/config.json"]
