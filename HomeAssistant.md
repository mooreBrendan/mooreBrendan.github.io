# Home Assistant

## Purpose
Home Assistant is a network automation tool.  It allows you to detect various events and run scripts when those events trigger.


## [[Docker]]
If you haven't already, click the link above to learn how to set up Docker.  Docker makes this service easier to setup and this guide will rely on it


## Setup


## Installation
```
services:
  homeassistant:
    container_name: homeassistant
    image: "homeassistant/home-assistant:stable"
    volumes:
      - ./config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
    privileged: true
```

## Verification
