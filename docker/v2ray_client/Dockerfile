FROM alpine:latest
LABEL maintainer="Hackxiu <hackxiu@gmail.com>"

ENV Tim=Asia/Shanghai
ENV CLIENT_ID "23ad6b10-8d1a-40f7-8ad0-e3e35cd38297"
ENV CLIENT_ALTERID 100
ENV CLIENT_WSPATH "/fuckgfw_letscrossgfw"
ENV VER=3.32

RUN set -ex \
        && apk --update \
	&& apk --no-cache add wget sed unzip daemon tzdata vim

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
	&& rm -rf /var/cache/apt/*

ADD config.json /etc/v2ray/
ENV PATH /usr/local/bin:$PATH

EXPOSE 1080
EXPOSE 8118

CMD ["v2ray", "-config=/etc/v2ray/config.json"]
