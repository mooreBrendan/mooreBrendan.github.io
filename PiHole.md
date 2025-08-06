# PiHole

## Purpose



## [[Docker]]
If you haven't already, click the link above to learn how to set up Docker.  Docker makes this service easier to setup and this guide will rely on it


## Setup


## Installation
```
services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    # For DHCP it is recommended to remove these ports and instead add: network_mode: host
    ports:
      - "53:53/tcp"
      - "53:53/udp"
    #   - "67:67/udp"
      - "8070:80/tcp"
      - "8073:443/tcp"
    environment:
      TZ: 'America/Indianapolis'
      PROXY_LOCATION: pihole
      VIRTUAL_HOST: pihole.domain
      VIRTUAL_PORT: 80
    volumes:
      - './etc-pihole:/etc/pihole'
      - './etc-dnsmasq.d:/etc/dnsmasq.d'
    cap_add:
      - NET_ADMIN # Recommended but not required (DHCP needs NET_ADMIN)    
    restart: unless-stopped
```

## Verification
