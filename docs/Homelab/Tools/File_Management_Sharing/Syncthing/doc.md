# Setting Up Syncthing with Docker Compose

## Introduction to Syncthing

Syncthing is an open-source continuous file synchronization program. It synchronizes files between two or more computers in real time, safely and efficiently.

## Docker Compose Configuration for Syncthing

This Docker Compose setup deploys Syncthing in a Docker container, ensuring a secure and isolated environment for file synchronization.

#### Docker Compose File (docker-compose.yml)

```
version: "2.1"
services:
  syncthing:
    image: lscr.io/linuxserver/syncthing:latest
    container_name: syncthing
    hostname: syncthing #optional
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - /path/to/appdata/config:/config
      - /path/to/data1:/data1
      - /path/to/data2:/data2
    ports:
      - 8384:8384
      - 22000:22000/tcp
      - 22000:22000/udp
      - 21027:21027/udp
    restart: unless-stopped
```

## Key Components of the Configuration

#### Environment Variables

* <code>PUID=1000</code> and <code>PGID=1000</code>: Sets user and group IDs for file permissions.

* <code>TZ=Etc/UTC</code>: Sets the container's timezone.

#### Volumes

* <code>/path/to/appdata/config:/config</code>: Maps the local config directory to the container's config directory.

* <code>/path/to/data1:/data1</code>: Maps the first local data directory to the container.

* <code>/path/to/data2:/data2</code>: Maps the second local data directory to the container.

#### Ports

* <code>8384:8384</code>: Web GUI.

* <code>22000:22000/tcp</code> and <code>22000:22000/udp</code>: Device communication.

* <code>21027:21027/udp</code>: Local network discovery.

#### Restart Policy

* <code>unless-stopped</code>: Ensures the container restarts automatically unless explicitly stopped.