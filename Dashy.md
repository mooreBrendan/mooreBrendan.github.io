# Dashy

## Purpose
Dashy is a service that offers a homepage for your homelab.  It allows you to link to the other various website that other homelab services use.  This enables you to not have to remember the various ip addresses or dns names.


## [[Docker]]
If you haven't already, click the link above to learn how to set up Docker.  Docker makes this service easier to setup and this guide will rely on it


## Setup


## Installation
The following is a sample docker compose file for running Dashy
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

## Initial Launch & testing
To launch the application, simply navigate to the folder with the Docker compose file, and then run Docker compose up.

*(note: Docker compose up can have an issue where you may be using the older "docker-compose" instead of the newer "docker compose".  The naming is similar, but are two different things.  You may have issues like I did where docker didn't have the correct repositories to install the newer Docker compose.  My [[Docker]] guide should have the correct info on how to fix this issue)*

Once the Docker container is up and running, you should be able to navigate to the page by typing into the url of your web browser the ip address of the server running the Docker container followed by a semi-colon ':' and then the port. this should be in the form of 'http://192.168.1.1:8080'