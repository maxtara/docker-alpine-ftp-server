# docker-alpine-ftp-server
[![Docker Stars](https://img.shields.io/docker/stars/delfer/alpine-ftp-server.svg)](https://hub.docker.com/r/delfer/alpine-ftp-server/) [![Docker Pulls](https://img.shields.io/docker/pulls/delfer/alpine-ftp-server.svg)](https://hub.docker.com/r/delfer/alpine-ftp-server/) [![Docker Automated build](https://img.shields.io/docker/automated/delfer/alpine-ftp-server.svg)](https://hub.docker.com/r/delfer/alpine-ftp-server/) [![Docker Build Status](https://img.shields.io/docker/build/delfer/alpine-ftp-server.svg)](https://hub.docker.com/r/delfer/alpine-ftp-server/) [![MicroBadger Layers](https://img.shields.io/microbadger/layers/delfer/alpine-ftp-server.svg)](https://hub.docker.com/r/delfer/alpine-ftp-server/) [![MicroBadger Size](https://img.shields.io/microbadger/image-size/delfer/alpine-ftp-server.svg)](https://hub.docker.com/r/delfer/alpine-ftp-server/)  
Small and flexible docker image with vsftpd server

## Usage
```
docker run -d \
    -p 21:21 \
    -p 21000-21010:21000-21010 \
    -e USERS="one|1234" \
    -e ADDRESS=ftp.site.domain \
    delfer/alpine-ftp-server
```

## Configuration

Environment variables:
- `USERS` - space and `|` separated list (optional, default: `ftp|alpineftp`)
  - format `name1|password1|[folder1][|uid1] name2|password2|[folder2][|uid2]`
- `ADDRESS` - external address witch clients can connect passive ports (optional)
- `MIN_PORT` - minimum port number to be used for passive connections (optional, default `21000`)
- `MAX_PORT` - maximum port number to be used for passive connections (optional, default `21010`)

## USERS examples

- `user|password foo|bar|/home/foo`
- `user|password|/home/user/dir|10000`
- `user|password||10000`
  
## docker-compose
```
  ftp:
    container_name: ftp
    image: maxtara/docker-alpine-ftp-server:latest
    restart: unless-stopped
    volumes:
      - /home/pi/ftp/:/home/user/ftp/:rw
    ports:
      - "2121:21"
      - "21000-21010:21000-21010"
    environment:
      - USERS=user|password|/home/user/ftp|1000
``` 
  
## Build
  
```
docker build -t docker-alpine-ftp-server .
# Deploy
docker tag docker-alpine-ftp-server maxtara/docker-alpine-ftp-server:latest
docker push maxtara/docker-alpine-ftp-server

```