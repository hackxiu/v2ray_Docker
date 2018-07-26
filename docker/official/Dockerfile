FROM debian:latest

LABEL maintainer "Darian Raymond <admin@v2ray.com>"

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV V2RAY_VERSION v3.31.1
ENV V2RAY_LOG_DIR /var/log/v2ray
ENV V2RAY_CONFIG_DIR /etc/v2ray/
ENV V2RAY_DOWNLOAD_URL https://github.com/v2ray/v2ray-core/releases/download/${V2RAY_VERSION}/v2ray-linux-64.zip

#更新apt-get源 使用163的源
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak &amp;&amp; \
    echo "deb http://mirrors.163.com/debian/ jessie main non-free contrib" &gt;/etc/apt/sources.list &amp;&amp; \
    echo "deb http://mirrors.163.com/debian/ jessie-proposed-updates main non-free contrib" &gt;&gt;/etc/apt/sources.list &amp;&amp; \
    echo "deb-src http://mirrors.163.com/debian/ jessie main non-free contrib" &gt;&gt;/etc/apt/sources.list &amp;&amp; \
    echo "deb-src http://mirrors.163.com/debian/ jessie-proposed-updates main non-free contrib" &gt;&gt;/etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y \
    bash \
    tzdata \
    curl \
    && mkdir -p \ 
        ${V2RAY_LOG_DIR} \
        ${V2RAY_CONFIG_DIR} \
        /tmp/v2ray \
    && curl -L -H "Cache-Control: no-cache" -o /tmp/v2ray/v2ray.zip ${V2RAY_DOWNLOAD_URL} \
    && unzip /tmp/v2ray/v2ray.zip -d /tmp/v2ray/ \
    && mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/v2ray /usr/bin \
    && mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/vpoint_vmess_freedom.json /etc/v2ray/config.json \
    && chmod +x /usr/bin/v2ray \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && rm -rf /tmp/v2ray /var/cache/*

ADD entrypoint.sh /entrypoint.sh

COPY config.json /etc/v2ray/config.json

ENV PATH /usr/bin/v2ray:$PATH

ENTRYPOINT ["/entrypoint.sh"]

CMD ["v2ray", "-config=/etc/v2ray/config.json"]
