# Setting Up Homepage with Docker Compose

## Introduction to Homepage

Homepage is a customizable start page or dashboard for your browser, designed to provide quick access to your frequently used websites, services, and tools.

## Docker Compose Configuration for Homepage

This Docker Compose setup deploys the Homepage application in a Docker container, allowing you to have a personalized start page for your browsing experience.

#### Docker Compose File (docker-compose.yml)

```yaml
version: "3.3"
services:
  homepage:
    image: ghcr.io/benphelps/homepage:latest
    container_name: homepage
    ports:
      - 3000:3000
    volumes:
      - ./config:/app/config # Make sure your local config directory exists
      - /var/run/docker.sock:/var/run/docker.sock:ro # (optional) For docker integrations
```

## Key Components of the Configuration

#### Service: Homepage

###### Image: 

* <code>ghcr.io/benphelps/homepage:latest</code> is the Docker image used for Homepage.

###### Ports:

* <code>3000:3000</code> maps port 3000 on the host to port 3000 in the container, where the Homepage web interface is accessible.

###### Volumes:

* <code>./config:/app/config</code>: Maps a local configuration directory to the container's configuration directory.

* <code>/var/run/docker.sock:/var/run/docker.sock:ro</code>: (Optional) Allows Homepage to integrate with Docker, provided read-only.

## Deploying Homepage

1. Ensure that the local <code>./config</code> directory exists and contains your configuration files.

2. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

3. Run <code>docker compose up -d</code> to start Homepage in detached mode.

4. Access Homepage by navigating to <code>http://<host-ip>:3000</code>.

## Configuring and Using Homepage

After deployment, you can customize Homepage through the configuration files in your local <code>./config</code> directory. This allows you to personalize the start page with your preferred links and services.