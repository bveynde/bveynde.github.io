---
title: Keeping portainer up to date with docker-compose
description: Portainer provides nice update commands when there is a new version, but I was
  looking for a docker-compose way...
date: 2022-07-14T09:36:34.304Z
preview: ""
draft: ""
tags:
  - docker
  - portainer
  - portainer-ce
  - docker-compose
categories:
  - docker
keywords:
  - docker
  - docker-compose
  - portainer
slug: keeping-portainer-uptodate-docker-compose
---
## Situation
Portainer provides nice update commands when there is a new version, but I was looking for a docker-compose way...

## Requirements
 * If nothing is selected, "9999 - tbd", must be the first choise
 * make sure the current name is in the list, even if it is inactive today
 * sort names alphabeticly 

## Short
```bash
docker-compose pull
docker-compose up --detach
```

## SETUP: make a docker container via docker-compose
My docker-compose.yml file:
```
# docker-compose.yml
version: '3'

services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    hostname: portainer
    restart: unless-stopped
    security_opt:
      - no-new-privileges:true
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ./data:/data
#    ports:
#      - 9000:9000

networks:
  default:
    name: dmz
```

 * I have created a network in docker called 'dmz'. This network hosts all systems that are behind my Nginx Proxy Manager. So all links are https-443 without using extra ports & I have a single selfsigned wildcard certificate to manage them all...
 * This reverse-proxy makes exposing local ports (9000) obsolete - they must now use the reverse-proxy
 * But enabeling this and restarting the portainer container is a nice backup plan if the reverse proxy is broken...
 * Don't forget to make a directory in the local dir.

## docker-compose up -d
 * And you should have a working portainer running on your docker...
 * That you cannot access from the outside if you have port 9000 disabled... ( so enable it the first time... ) 

## Upgrading
### docker-compose pull
 * Download the latest image
 * Please note the "image: portainer/portainer-ce:latest" line, do not expect an new version if you staticly defined a fixed version here
 * Docker has downloaded the most recent version, your container is still running with that previous version... 
### docker-compose up --detach
 * In docker-compose terms is this a reboot of your container...
 * As there now is a newer image available, you have upgraded your system
 * If the previous command did not download a new image, there is no reason to run this command
 * Please note that some tools/containers will require you to run migration commands when upgrading...

## Still to be Fixed
 * Running portainer behind a Nginx Proxy Manager works fine, but the possibility to open a shell does not work via the portainer web interface. 
 * It was not that easy as just enabeling port 8000 as a stream...
 * This is a Nginx config issue (Read: Bart issue) and does not change anything about this post to upgrade containers via docker-compose...
 * If you have this working, please contact me !

## Ref
 * [stackoverflow - Evgen Bodunov answer](https://stackoverflow.com/questions/49316462/how-to-update-existing-images-with-docker-compose)

 