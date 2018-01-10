FROM hypriot/rpi-alpine
MAINTAINER John Stafford <john@jkms.me>

RUN apk add --update nodejs bash python git build-base linux-headers

ADD . /src

RUN adduser -D -h /etc/cjdns -u 1000 cjdns \
    && rm -rf /src/build_* && cd /src \
    && NO_TEST=1 Seccomp_NO=1 ./do && cd / \
    && cp /src/cjdroute /usr/bin \
    && cp -r /src/tools/* /usr/bin \
    && cp /src/makekeys \
          /src/privatetopublic \
          /src/makekeys \
          /src/randombytes \
          /src/sybilsim /usr/bin \
    && cp /src/contrib/docker/entrypoint.sh / \
    && rm -rf /src /var/cache/apk/* \
    && apk del --purge python build-base linux-headers

VOLUME [ "/etc/cjdns" ]

ENTRYPOINT [ "/entrypoint.sh" ]
