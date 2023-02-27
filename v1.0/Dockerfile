FROM alpine:3.17
LABEL maintainer="piny00"
LABEL build_date="2023-02-26"

RUN apk update && apk add openrc tzdata unbound
COPY unbound.conf /etc/unbound/unbound.conf

RUN cp /usr/share/zoneinfo/Europe/Budapest /etc/localtime \
    && echo "Europe/Budapest" >  /etc/timezone \
    && apk del tzdata \
    && rc-update add unbound \
    && touch /run/openrc/softlevel \
    && touch /var/log/unbound.log \
    && chown unbound:unbound /var/log/unbound.log
    && rc-service unbound start

EXPOSE 53/udp 53/tcp
CMD ["/bin/sh"]
