# wireguard-docker
wireguard docker implementation for debian stretch

*Basics*:
* install wireguard and its kernel-modules on the host first
* place/edit wireguard config files in /etc/wireguard in host fs
* NO iptables rules in e.g. /etc/wireguard/wg0.conf necessary they are handled by the Dockerfile
* modify incomming port in docker-compose.yal if you want to change it (port 443/udp by default)
* everything else is managed by docker and the compose script -> run it using docker-compose up -d

*Other Stuff*:
* _unbound_ is running as dns service in the container. Use _DNS_ option in the client config-file to set the DNS-Server to the IP configured for the server tunnel interface (e.g. DNS=10.100.100.1).  

*Sample Client Config*
```
[Interface]
Address = 10.100.100.2/24
PrivateKey = <PrivKEy goes here>
DNS = 10.100.100.1

[Peer]
PublicKey = <PubKey goes here>
#FullTunnel Mode
AllowedIPs = 0.0.0.0/0
Endpoint = 1.2.3.4:443
PersistentKeepalive = 25
```

*Sample Server Config*
```
[Interface]
Address = 10.100.100.1/24
ListenPort = 5555
PrivateKey = <PrivKEy goes here>

[Peer]
PublicKey = <PubKey goes here>
AllowedIPs = 10.100.100.2/32
```

Credits to:
* https://github.com/cmulk/wireguard-docker
* https://www.ckn.io/blog/2017/11/14/wireguard-vpn-typical-setup/
