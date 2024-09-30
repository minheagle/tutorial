# Setting Up Watchtower with Docker Compose

## Introduction to Watchtower

Watchtower is an application that automatically updates your running Docker containers to the latest images. It monitors all containers and updates them in real-time whenever a new image is released.

## Docker Compose Configuration for Watchtower

This Docker Compose setup deploys Watchtower in a Docker container, ensuring your other containers are always up-to-date with the least amount of hassle.

#### Docker Compose File (docker-compose.yml)

```yaml
version: '3'
services:
  watchtower:
    image: containrrr/watchtower
    command:
      - --cleanup=true
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

#### Key Components of the Configuration

###### **Image**

* <code>containrrr/watchtower</code>: The Docker image used for Watchtower.

###### **Command**

* <code>--cleanup=true</code>: Enables cleanup of old images after updating.

###### **Restart Policy**

* <code>always</code>: Ensures the Watchtower container restarts automatically after a crash or reboot.

###### **Volumes**

* <code>/var/run/docker.sock:/var/run/docker.sock</code>: Mounts the Docker socket so Watchtower can interact with the Docker daemon.

## Deploying Watchtower

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> to start Watchtower in detached mode.

## How Watchtower Works

Once deployed, Watchtower automatically checks for updates to the images of all running containers at the specified interval. If a new image is found, Watchtower updates the container without downtime.

Remember to ensure that your containers are configured to handle updates gracefully!
