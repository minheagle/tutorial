# Setting Up Logitech Media Server with Docker Compose

## Introduction to Logitech Media Server

Logitech Media Server (LMS) is a software that powers audio streaming to Logitech Squeezebox players. It allows you to listen to your music collection anywhere in your home, controlling it with a mobile device or computer.

## Docker Compose Configuration for LMS

This Docker Compose setup deploys Logitech Media Server in a Docker container, ensuring a reliable and dedicated environment for your music streaming needs.

#### Docker Compose File (docker-compose.yml)

```
version: '3'
services:
  lms:
    container_name: lms
    image: lmscommunity/logitechmediaserver
    volumes:
      - /<somewhere>:/config:rw
      - /<somewhere>:/music:ro
      - /<somewhere>:/playlist:rw
      - /etc/localtime:/etc/localtime:ro
      - /etc/timezone:/etc/timezone:ro
    ports:
      - 9000:9000/tcp
      - 9090:9090/tcp
      - 3483:3483/tcp
      - 3483:3483/udp
    restart: always
```

## Key Components of the Configuration

#### Volumes

* <code>/<somewhere>:/config:rw</code>: Maps the local configuration directory to the container's configuration directory.
* <code>/<somewhere>:/music:ro</code>: Maps the local music directory to the container, read-only.
* <code>/<somewhere>:/playlist:rw</code>: Maps the local playlist directory to the container.
* <code>/etc/localtime:/etc/localtime:ro</code>: Maps the local time setting for correct time display.
* <code>/etc/timezone:/etc/timezone:ro</code>: Ensures the container uses the correct timezone.

#### Ports

* <code>9000:9000/tcp</code>: Web interface.
* <code>9090:9090/tcp</code>: CLI port.
* <code>3483:3483/tcp</code> and <code>3483:3483/udp</code>: Used for streaming and device discovery.

#### Restart Policy

* <code>always</code>: Ensures LMS restarts automatically unless manually stopped.

## Deploying LMS

1. Replace <code>/<somewhere></code> with your actual directory paths in the Docker Compose file.
2. Save the configuration in a <code>docker-compose.yml</code> file.
3. Run <code>docker compose up -d</code> to start the LMS container in detached mode.
4. Access the LMS web interface via <code>http://<host-ip>:9000</code>.

## Configuring and Using LMS
After deployment, configure your music libraries, playlists, and settings via the LMS web interface. Connect your Squeezebox devices or compatible software players to start streaming your music.