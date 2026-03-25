# Obsidian

## Purpose
Obsidian is a note taking app that use markdown files.  you can use this for simple note taking, but I use it to make the base for the wepages you are looking at right now


## [[Docker]]
If you haven't already, click the link above to learn how to set up Docker.  Docker makes this service easier to setup and this guide will rely on it

## Installation
```
services:
  obsidian:
    image: 'ghcr.io/sytone/obsidian-remote:latest'
    container_name: obsidian
    restart: unless-stopped
    volumes:
      - ./vaults:/vaults # The location on the host for your Obsidian Vaults
      - ./obsidian.json:/config/.config/obsidian/obsidian.json # The location to store Obsidan configuration and ssh data for obsidian-git
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Ameria/Indianapolis
      - DOCKER_MODS=linuxserver/mods:universal-git # Use to add mods to the container like git.
      - KEYBOARD=en-us-qwerty # Used to set the keyboard being used for input. E.g. KEYBOARD=en-us-qwerty or KEYBOARD=de-de-qwertz
```

## Verification

## Issues
