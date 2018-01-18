FROM hypriot/rpi-alpine as builder
MAINTAINER John Stafford <john@jkms.me>

RUN apk add --update nodejs bash python git build-base linux-headers

ADD . /src

RUN adduser -D -h /etc/cjdns -u 1000 cjdns \
    && rm -rf /src/build_* && cd /src \
    && NO_TEST=1 Seccomp_NO=1 ./do 

FROM hypriot/rpi-alpine
MAINTAINER John Stafford <john@jkms.me>

RUN apk add --update nodejs bash

COPY --from=builder /src/cjdroute /usr/bin 
COPY --from=builder /src/tools/ /usr/bin
COPY --from=builder /src/makekeys /usr/bin
COPY --from=builder /src/privatetopublic /usr/bin
COPY --from=builder /src/makekeys /usr/bin
COPY --from=builder /src/randombytes /usr/bin
COPY --from=builder /src/sybilsim /usr/bin
COPY --from=builder /src/contrib/docker/entrypoint.sh /


VOLUME [ "/etc/cjdns" ]

ENTRYPOINT [ "/entrypoint.sh" ]
