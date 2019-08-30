FROM debian:stretch

RUN echo "deb http://deb.debian.org/debian/ unstable main" > /etc/apt/sources.list.d/unstable-wireguard.list && \
 printf 'Package: *\nPin: release a=unstable\nPin-Priority: 90\n' > /etc/apt/preferences.d/limit-unstable

RUN apt update && \
 apt install -y --no-install-recommends wireguard-tools iptables && \
 apt clean

WORKDIR /scripts
ENV PATH="/scripts:${PATH}"
COPY scripts/install-module.sh /scripts
COPY scripts/entrypoint.sh /scripts
RUN chmod 755 /scripts/*

CMD ["entrypoint.sh"]
