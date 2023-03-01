FROM alpine:3.17
LABEL maintainer="piny00"
LABEL build_date="2023-02-26"

RUN apk update && apk add tzdata unbound
COPY unbound.conf /etc/unbound/
COPY start.sh /

EXPOSE 53/udp 53/tcp

RUN cp /usr/share/zoneinfo/Europe/Budapest /etc/localtime \
    && echo "Europe/Budapest" >  /etc/timezone \
    && apk del tzdata \
    && touch /var/log/unbound.log \
    && chown unbound:unbound /var/log/unbound.log \
    && chmod +x /start.sh

CMD [ "/start.sh" ]

