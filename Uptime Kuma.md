# Uptime Kuma

## Purpose



## [[Docker]]
If you haven't already, click the link above to learn how to set up Docker.  Docker makes this service easier to setup and this guide will rely on it


## Setup
```
services:
  uptime_kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    volumes:
      - uptime-kuma:/app/data
    restart: always

volumes:
  uptime-kuma:
```

## Installation


## Verification
