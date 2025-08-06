## Dashy

## Purpose



## [[Docker]]
If you haven't already, click the link above to learn how to set up Docker.  Docker makes this service easier to setup and this guide will rely on it


## Setup


## Installation
```
services:
  dashy:
    image: lissy93/dashy
    container_name: dashy
    
    # Pass in your config file below, by specifying the path on your host machine    
    volumes:
      - "./config.yml:/app/user-data/conf.yml"
    environment:
      - NODE_ENV=production
      # Specify your user ID and group ID. You can find this by running `id -u` and `id -g`    
      - UID=1000
      - GID=1000
    restart: unless-stopped

    # Configure healthchecks
    healthcheck:
      test: [ 'CMD', 'node', '/app/services/healthcheck' ]
      interval: 1m30s
      timeout: 10s
      retries: 3
      #start_period: 40s
```

## Verification