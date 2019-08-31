FROM debian:stretch

#Add repositories needed for wireguard
RUN echo "deb http://deb.debian.org/debian/ unstable main" > /etc/apt/sources.list.d/unstable-wireguard.list && \
 printf 'Package: *\nPin: release a=unstable\nPin-Priority: 90\n' > /etc/apt/preferences.d/limit-unstable

#Upgrade packages and install needed ones
RUN apt update && \
 apt upgrade -y && \
 apt install -y --no-install-recommends wireguard-tools iptables unbound unbound-host curl && \
 apt clean

#Download root hints for unbound
RUN curl -o /var/lib/unbound/root.hints https://www.internic.net/domain/named.cache

#Configure log and set permissions for unbound deamon
touch /etc/unbound/unbound.log && \
 chown unbound:unbound /etc/unbound/unbound.log && \
 chown -R unbound:unbound /var/lib/unbound

#Copy stuff to container
WORKDIR /scripts
ENV PATH="/scripts:${PATH}"
COPY scripts/entrypoint.sh /scripts
RUN chmod 755 /scripts/*
COPY config/unbound.conf /etc/unbound

#Run the services
CMD ["entrypoint.sh"]
