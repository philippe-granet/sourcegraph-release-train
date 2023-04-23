# sourcegraph-oss-release-train

[![Docker Image Version (latest semver)](https://img.shields.io/docker/v/philippegranet/sourcegraph-server-oss?sort=semver)][docker_hub]
[![Docker Image Size (latest semver)](https://img.shields.io/docker/image-size/philippegranet/sourcegraph-server-oss?sort=semver)][docker_hub]
![Docker Pulls](https://img.shields.io/docker/pulls/philippegranet/sourcegraph-server-oss)

[![Docker Image Version (latest semver)](https://img.shields.io/docker/v/sourcegraph/server?color=orange&label=sourcegraph%20enterprise%20version&logo=sourcegraph&sort=semver)][docker_sg]
![Docker Pulls](https://img.shields.io/docker/pulls/sourcegraph/server?color=orange&label=enterprise%20docker%20pulls&logo=docker)

[![Release train](https://github.com/philippe-granet/sourcegraph-release-train/actions/workflows/release_train.yml/badge.svg)][gh_actions]

This repo just creates a build pipeline on top of [sourcegraph](https://github.com/sourcegraph/sourcegraph)-OSS.
The [enterprise version](https://hub.docker.com/r/sourcegraph/server) is great, but I cannot afford it beyond the trial, and since I like automating things,  
I thought I'd automate the release pipeline for the OSS docker image.

## Simple run conf
```shell
mkdir -p ~/.sourcegraph/config
mkdir -p ~/.sourcegraph/data

docker run -d \
  --publish 7080:7080 \
  --publish 127.0.0.1:3370:3370 \
  --volume ~/.sourcegraph/config:/etc/sourcegraph \
  --volume ~/.sourcegraph/data:/var/opt/sourcegraph \
  --name sourcegraph \
  jensim/sourcegraph-server-oss:latest
```

## docker-compose.yml
```yaml
version: '3.3'

services:
  sourcegraph:
    image: jensim/sourcegraph-server-oss:latest
    ports:
      - "7080:7080"
    volumes:
      - .sourcegraph/config:/etc/sourcegraph
      - .sourcegraph/data:/var/opt/sourcegraph
      - .sourcegraph/site-conf:/root
```

[docker_hub]: https://hub.docker.com/r/philippegranet/sourcegraph-server-oss/tags?page=1&ordering=last_updated
[gh_actions]: https://github.com/philippe-granet/sourcegraph-release-train/actions/workflows/release_train.yml
[docker_sg]: https://hub.docker.com/r/sourcegraph/server
