FROM alpine:3.17
LABEL maintainer="piny00"
LABEL build_date="2023-02-26"

VOLUME [ "/sys/fs/cgroup" ]

RUN apk update && apk add openrc tzdata unbound
COPY unbound.conf /etc/unbound/
COPY start.sh /

EXPOSE 53/udp 53/tcp

RUN rc-update -u \
    && cp /usr/share/zoneinfo/Europe/Budapest /etc/localtime \
    && echo "Europe/Budapest" >  /etc/timezone \
    && apk del tzdata \
    && rc-update add unbound \
    && touch /run/openrc/softlevel \
    && touch /var/log/unbound.log \
    && chown unbound:unbound /var/log/unbound.log \
    && chmod +x /start.sh

CMD [ "/start.sh" ]
