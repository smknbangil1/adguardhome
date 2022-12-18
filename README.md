## install adguardhome using docker on ubuntu 22.04 LTS (by maspur)
##
### update package
###
### install docker dan docker compose
###
bikin direktori /volume/docker/adguard/work dan.... /volume/docker/adguard/conf
###
```bash
version: '3.3'
services:
  adguardhome:
    image: adguard/adguardhome
    restart: unless-stopped
    volumes:
      - type: bind
        source: /volume/docker/adguard/work
        target: /opt/adguardhome/work
      - type: bind
        source: /volume/docker/adguard/conf
        target: /opt/adguardhome/conf
    ports:
      - '53:53/tcp'
      - '53:53/udp'
      - '80:80/tcp'
      - '443:443/tcp'
      - '443:443/udp'
      - '3000:3000/tcp'
```
###
Edit : /etc/systemd/resolved.conf
###
[Resolve]
DNS=127.0.0.1
DNSStubListener=no
###
mv /etc/resolv.conf /etc/resolv.conf.ori
###
ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
###
###
Restart systemd-resolved:
systemctl restart systemd-resolved
###
optmasi dns adguard
https://cln.io/blog/adguard-parallel-requests/
###
