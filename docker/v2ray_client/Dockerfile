FROM alpine:latest
LABEL maintainer="Hackxiu <hackxiu@gmail.com>"

ENV Tim=Asia/Shanghai
ENV CLIENT_ID "23ad6b10-8d1a-40f7-8ad0-e3e35cd38297"
ENV CLIENT_ALTERID 100
ENV CLIENT_WSPATH "/fuckgfw_letscrossgfw"
ENV VER=4.5.0

RUN apk add --no-cache ca-certificates && update-ca-certificates
RUN apk update
RUN apk --no-cache upgrade
RUN apk add -U --no-cache wget bash tzdata unzip vim sed privoxy supervisor

RUN wget --no-check-certificate -O v2ray.zip https://github.com/v2ray/v2ray-core/releases/download/v$VER/v2ray-linux-64.zip \
    && unzip v2ray.zip \
    && mv ./v2ray-v$VER-linux-64/v2ray /usr/local/bin/ \
    && mv ./v2ray-v$VER-linux-64/v2ctl /usr/local/bin/ \
    && mv ./v2ray-v$VER-linux-64/geosite.dat /usr/local/bin/ \
    && mv ./v2ray-v$VER-linux-64/geoip.dat /usr/local/bin/ \
    && chmod 777 /usr/local/bin/v2ctl \
    && chmod 777 /usr/local/bin/v2ray \
    && chmod 777 /usr/local/bin/geosite.dat \
    && chmod 777 /usr/local/bin/geoip.dat \
    && rm -rf v2ray.zip \
    && rm -rf v2ray-v$VER-linux-64

RUN mkdir /var/log/v2ray \
    && echo ${Tim} > /etc/timezone \
    && mkdir /etc/v2ray \
    && chmod -R 777 /var/log/v2ray \
    && chmod -R 777 /etc/v2ray \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apk/*

ADD privoxy_config /etc/privoxy/config

RUN sed -i -e '/^listen-address/s/127.0.0.1/0.0.0.0/' \
    -e '/^accept-intercepted-requests/s/0/1/' \
    -e '/^enforce-blocks/s/0/1/' \
    -e '/^#debug/s/#//' /etc/privoxy/config

ADD config.json /etc/v2ray/
ADD supervisord.conf /etc/supervisor/conf.d/
ENV PATH /usr/local/bin:$PATH

EXPOSE 1080
EXPOSE 8118

CMD ["supervisord", "--nodaemon", "--configuration", "/etc/supervisor/conf.d/supervisord.conf"]
