# Setting Up Excalidraw with Docker Compose

## Introduction to Excalidraw

Excalidraw is a virtual collaborative whiteboard tool that lets you easily sketch diagrams with a hand-drawn feel. It's designed to be simple, intuitive, and to allow rapid collaboration.

## Docker Compose Configuration for Excalidraw

This Docker Compose setup deploys Excalidraw in a Docker container, offering an isolated environment for your sketching and collaboration needs.

#### Docker Compose File (docker-compose.yml)

```yaml
version: "3.8"

services:
  excalidraw:
    container_name: excalidraw
    image: excalidraw/excalidraw:latest
    ports:
      - "80:80"
    restart: on-failure
```

## Key Components of the Configuration

#### Service: Excalidraw

###### Image: 

* <code>excalidraw/excalidraw:latest</code> is the Docker image used for Excalidraw.

###### Ports:

* <code>80:80</code> maps port 80 on the host to port 80 in the container, where Excalidraw's web interface is accessible.

###### Restart Policy: 

* <code>on-failure</code> ensures that the Excalidraw service restarts automatically in case of failure.

## Deploying Excalidraw

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> to start Excalidraw in detached mode.

3. Access Excalidraw by navigating to <code>http://<host-ip>:80</code>.

## Configuring and Using Excalidraw

After deployment, Excalidraw is ready to use through its web interface, providing a collaborative platform for sketching and diagramming.

