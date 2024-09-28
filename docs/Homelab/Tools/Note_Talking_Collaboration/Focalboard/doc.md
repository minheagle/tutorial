# Setting Up Focalboard with Docker Compose

## Introduction to Focalboard

Focalboard is an open-source, self-hosted project management tool that's an alternative to Trello, Notion, and Asana. It's designed to help teams stay organized and aligned.

## Docker Compose Configuration for Focalboard

This Docker Compose setup deploys Focalboard in a Docker container, providing a straightforward and efficient environment for project management.

#### Docker Compose File (docker-compose.yml)

```
version: "3.3"
services:
  focalboard:
    ports:
      - 8000:8000
    restart: always
    image: mattermost/focalboard
```

## Key Components of the Configuration

#### Service: Focalboard

###### Image: 

* <code>mattermost/focalboard</code> is used to pull the latest Focalboard image.

###### Ports:

* <code>8000:8000</code> exposes Focalboard on port 8000, both on the host and inside the container.

###### Restart Policy: 

* <code>always</code> ensures that the Focalboard service restarts automatically after a crash or reboot.

## Deploying Focalboard

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.
2. Run <code>docker compose up -d</code> to start Focalboard in detached mode.
3. Access Focalboard by navigating to <code>http://<host-ip>:8000</code>.

## Configuring and Using Focalboard

After deployment, you can begin using Focalboard by creating boards, adding tasks, and managing projects directly through the web interface.