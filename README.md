# wireguard-docker
wireguard docker implementation fpr debian stretch based on https://github.com/cmulk/wireguard-docker

* place/edit wireguard config files in /etc/wireguard in host fs
* NO iptables rules in e.g. /etc/wireguard/eg0.conf necessarym they are handled by the Dockerfile
* modify incomming port in docker-compose.yaml if you want to change it (port 443/udp default)
* everything else is managed by docker and the compose script -> run it using docker-compose up -d
