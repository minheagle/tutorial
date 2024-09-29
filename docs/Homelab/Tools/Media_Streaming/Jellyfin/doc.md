# Setting Up Jellyfin with Docker Compose

## Introduction to Jellyfin

Jellyfin is a free and open-source media solution that allows you to organize, manage, and share your media files. It is an alternative to services like Plex or Emby, offering no subscription fees and a completely customizable and private experience.

## Docker Compose Configuration for Jellyfin

This Docker Compose setup deploys Jellyfin in a Docker container, ensuring a consistent and isolated environment. The configuration includes custom volume paths and environment settings.

#### Docker Compose File (docker-compose.yml)

```yaml
version: "2.1"
services:
  jellyfin:
    image: lscr.io/linuxserver/jellyfin:latest
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Pacific/Auckland
    volumes:
      - /home/server/jellyfin/library:/config
      - /home/server/jellyfin/tvseries:/data/tvshows
      - /home/server/jellyfin/movies:/data/movies
    ports:
      - 8096:8096
      - 8920:8920 #optional
      - 7359:7359/udp #optional
      - 1900:1900/udp #optional
    restart: unless-stopped
```

## Key Components of the Configuration

#### Environment Variables

* <code>PUID=1000</code> and <code>PGID=1000</code>: Set user and group IDs for file permissions.

* <code>TZ=Pacific/Auckland</code>: Sets the container's timezone.

#### Volumes

* <code>/home/server/jellyfin/library:/config</code>: Configuration and data storage.

* <code>/home/server/jellyfin/tvseries:/data/tvshows</code>: TV series library.

* <code>/home/server/jellyfin/movies:/data/movies</code>: Movies library.

#### Ports

* <code>8096:8096</code>: Main access port for Jellyfin's web interface.

* <code>8920:8920</code>: Optional port for HTTPS access.

* <code>7359:7359/udp</code>: Optional port for live TV and DVR features.

* <code>1900:1900/udp</code>: Optional port for DLNA.

#### Restart Policy

* <code>unless-stopped</code>: The container restarts automatically after a crash, except when it has been explicitly stopped.

## Deploying Jellyfin

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> to start Jellyfin in detached mode.

3. Access Jellyfin's web interface via <code>http://<host-ip>:8096</code>.

## Configuring and Using Jellyfin

Once deployed, you can configure Jellyfin through its web interface, including setting up media libraries, user accounts, and streaming settings.