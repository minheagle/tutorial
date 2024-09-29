# Setting Up FreshRSS with Docker Compose

## Introduction to FreshRSS

FreshRSS is a self-hosted RSS feed aggregator. It is lightweight, easy to work with, and allows you to keep all your favorite news feeds and blogs organized in one place.

## Docker Compose Configuration for FreshRSS

This Docker Compose setup deploys FreshRSS in a Docker container, providing an isolated and efficient environment for managing your RSS feeds.

#### Docker Compose File (docker-compose.yml)

```yaml
version: "2.1"
services:
  freshrss:
    image: lscr.io/linuxserver/freshrss:latest
    container_name: freshrss
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
    volumes:
      - /path/to/data:/config 
    ports:
      - 80:80 
    restart: unless-stopped
```

## Key Components of the Configuration

#### Environment Variables

* <code>PUID=1000</code> and <code>PGID=1000</code>: Set user and group IDs for file permissions.

* <code>TZ=Etc/UTC</code>: Sets the container's timezone.

#### Volumes

* <code>/path/to/data:/config</code>: Maps the local data directory to the container's configuration directory.

#### Ports

* <code>80:80</code>: Maps port 80 of the host to port 80 of the container, allowing web access to FreshRSS.

#### Restart Policy

* <code>unless-stopped</code>: Ensures the container restarts automatically unless explicitly stopped.

## Deploying FreshRSS

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Replace <code>/path/to/data</code> with your desired local directory path.

3. Run <code>docker compose up -d</code> to start FreshRSS in detached mode.

4. Access FreshRSS via <code>http://<host-ip></code>.

## Configuring and Using FreshRSS

After deployment, access the FreshRSS web interface to configure your feeds, categories, and reading preferences. Ensure you manage user accounts and settings as required.