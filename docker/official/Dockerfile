FROM debian:latest

LABEL maintainer="Darian Raymond <admin@v2ray.com>"

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV V2RAY_VERSION v3.31.1
ENV V2RAY_LOG_DIR /var/log/v2ray
ENV V2RAY_CONFIG_DIR /etc/v2ray/
ENV V2RAY_DOWNLOAD_URL https://github.com/v2ray/v2ray-core/releases/download/${V2RAY_VERSION}/v2ray-linux-64.zip

RUN apt-get update && apt-get install -y wget curl apt-utils tar unzip openssl curl sed net-tools iptables

ADD entrypoint.sh /entrypoint.sh
COPY config.json /etc/v2ray/config.json
ENV PATH /usr/bin/v2ray:$PATH

CMD ["v2ray", "-config=/etc/v2ray/config.json"]

ENTRYPOINT ["/entrypoint.sh"]
