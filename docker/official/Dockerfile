FROM debian:latest

LABEL maintainer="Darian Raymond <admin@v2ray.com>"

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV V2RAY_VERSION v3.31.1
ENV V2RAY_LOG_DIR /var/log/v2ray
ENV V2RAY_CONFIG_DIR /etc/v2ray/
ENV V2RAY_DOWNLOAD_URL https://github.com/v2ray/v2ray-core/releases/download/${V2RAY_VERSION}/v2ray-linux-64.zip

COPY config.json /etc/v2ray/config.json

RUN apt-get update && apt-get install -y wget curl apt-utils tar unzip daemon openssl curl sed net-tools vim \
    && mkdir -p \
    ${V2RAY_LOG_DIR} \
    ${V2RAY_CONFIG_DIR} \
    /tmp/v2ray \
    /usr/bin/v2ray \
    /var/log/v2ray/ \
    && curl -L -H "Cache-Control: no-cache" -o /tmp/v2ray/v2ray.zip ${V2RAY_DOWNLOAD_URL} \
    && unzip /tmp/v2ray/v2ray.zip -d /tmp/v2ray/ \
    && mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/v2ray /usr/bin/v2ray \
    && mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/v2ctl /usr/bin/v2ray \
    && mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/geoip.dat /usr/bin/v2ray \
    && mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/geosite.dat /usr/bin/v2ray \
    && mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/v2ctl.sig /usr/bin/v2ray \
    && mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/v2ray.sig /usr/bin/v2ray \
    && mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/vpoint_vmess_freedom.json /etc/v2ray/config.json \
    && chmod +x /usr/bin/v2ray/v2ray \
    && chmod +x /usr/bin/v2ray/v2ctl \
    && chmod +x /usr/bin/v2ray/geoip.dat \
    && chmod +x /usr/bin/v2ray/geosite.dat \
    && chmod +x /usr/bin/v2ray/v2ctl.sig \
    && chmod +x /usr/bin/v2ray/v2ray.sig \
    && chmod +x /etc/v2ray/config.json \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && rm -rf /tmp/v2ray /var/cache/*

ENV PATH /usr/bin/v2ray/v2ray:$PATH

CMD ["v2ray", "-config=/etc/v2ray/config.json"]
