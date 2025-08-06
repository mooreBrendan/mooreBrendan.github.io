# NTFY

## Purpose



## [[Docker]]
If you haven't already, click the link above to learn how to set up Docker.  Docker makes this service easier to setup and this guide will rely on it


## Setup



## Installation
```
services:
  ntfy:
    image: binwiederhier/ntfy
    container_name: ntfy
    command:
      - serve
    environment:
      NTFY_BASE_URL: http://ntfy.domain
    volumes:
      - /var/cache/ntfy:/var/cache/ntfy
      - ./etc:/etc/ntfy
    healthcheck:
      test: [ "CMD-SHELL", "wget -q --tries=1 http://127.0.0.1/v1/health -O - | grep -Eo '\"healthy\"\\s*:\\s*true' || exit 1" ]
      interval: 60s
      timeout: 10s
      retries: 3
      start_period: 40s
    restart: unless-stopped
```

## Verification

`curl -d "message" -k -L ntfy.domain/topic`