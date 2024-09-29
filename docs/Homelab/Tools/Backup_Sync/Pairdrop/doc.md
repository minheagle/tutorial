# Setting Up Pairdrop with Docker Compose

## Introduction to Pairdrop

Pairdrop is an application designed for simple and secure file sharing. It's a self-hosted solution that allows easy file transfers within a network.

## Docker Compose Configuration for Pairdrop

This Docker Compose setup deploys Pairdrop in a Docker container, providing a secure and isolated environment for file sharing.

#### Docker Compose File (docker-compose.yml)

```yaml
version: "2.1"
services:
  pairdrop:
    image: lscr.io/linuxserver/pairdrop:latest
    container_name: pairdrop
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - RATE_LIMIT=false #optional
      - WS_FALLBACK=false #optional
      - RTC_CONFIG= #optional
      - DEBUG_MODE=false #optional
    ports:
      - 3000:3000
    restart: unless-stopped
```

#### Environment Variables

* <code>PUID=1000</code> and <code>PGID=1000</code>: Sets user and group IDs for file permissions.

* <code>TZ=Etc/UTC</code>: Configures the container's timezone.

* <code>RATE_LIMIT=false</code>: (Optional) Disables rate limiting.

* <code>WS_FALLBACK=false</code>: (Optional) Disables WebSocket fallback.

* <code>RTC_CONFIG</code>: (Optional) WebRTC configuration.

* <code>DEBUG_MODE=false</code>: (Optional) Disables debug mode.

#### Ports

* <code>3000:3000</code>: Maps port 3000 of the host to port 3000 of the container, enabling web access to Pairdrop.

#### Restart Policy

* <code>unless-stopped</code>: Ensures the container restarts automatically unless explicitly stopped.

## Key Components of the Configuration

#### Environment Variables

* <code>PUID=1000</code> and <code>PGID=1000</code>: Sets user and group IDs for file permissions.

* <code>TZ=Etc/UTC</code>: Configures the container's timezone.

* <code>RATE_LIMIT=false</code>: (Optional) Disables rate limiting.

* <code>WS_FALLBACK=false</code>: (Optional) Disables WebSocket fallback.

* <code>RTC_CONFIG</code>: (Optional) WebRTC configuration.

* <code>DEBUG_MODE=false</code>: (Optional) Disables debug mode.

#### Ports

* <code>3000:3000</code>: Maps port 3000 of the host to port 3000 of the container, enabling web access to Pairdrop.

#### Restart Policy

* <code>unless-stopped</code>: Ensures the container restarts automatically unless explicitly stopped.