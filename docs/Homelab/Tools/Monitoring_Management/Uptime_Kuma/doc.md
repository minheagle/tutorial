# Setting Up Uptime Kuma with Docker Compose

## Introduction to Uptime Kuma

Uptime Kuma is a self-hosted monitoring tool similar to "Uptime Robot." It monitors your websites, services, and applications and provides uptime notifications.

## Docker Compose Configuration for Uptime Kuma

This Docker Compose setup deploys Uptime Kuma in a Docker container, providing a reliable environment for monitoring your services.

#### Docker Compose File (docker-compose.yml)

```yaml
version: '3'
services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    restart: always
    ports:
      - "3010:3001"
    volumes:
      - uptime-kuma:/app/data
      - /var/run/docker.sock:/var/run/docker.sock

volumes:
  uptime-kuma:
```

## Key Components of the Configuration

#### Service: Uptime Kuma

###### **Image**: 

* <code>louislam/uptime-kuma:1</code> is the Docker image for Uptime Kuma.

###### **Ports**:

* <code>3010:3001</code> maps port 3010 on the host to port 3001 in the container, where Uptime Kuma's web interface is accessible.

###### **Volumes**:

* <code>uptime-kuma:/app/data</code> is used for persistent storage of Uptime Kuma data.

* <code>/var/run/docker.sock:/var/run/docker.sock</code> allows Uptime Kuma to monitor Docker containers.

###### **Restart Policy**: 

* <code>always</code> ensures that Uptime Kuma restarts automatically after a crash or reboot.

## Deploying Uptime Kuma

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> to start Uptime Kuma in detached mode.

3. Access Uptime Kuma's web interface via <code>http://host-ip:3010</code>.

## Configuring and Using Uptime Kuma

After deployment, you can configure Uptime Kuma through its web interface to monitor your websites and services, set up notifications, and track uptime and response times.

