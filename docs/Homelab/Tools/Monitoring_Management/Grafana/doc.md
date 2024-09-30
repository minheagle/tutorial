# Setting Up Grafana with Docker Compose

## Introduction to Grafana

Grafana is an open-source platform for monitoring and observability. It allows you to query, visualize, alert on, and understand your metrics no matter where they are stored.

## Docker Compose Configuration for Grafana

This Docker Compose setup deploys Grafana in a Docker container, providing a powerful and flexible way to visualize and analyze your data.

#### Docker Compose File (docker-compose.yml)

```yaml
version: "3.8"
services:
  grafana:
    image: grafana/grafana
    container_name: grafana
    restart: unless-stopped
    ports:
     - '3000:3000'
    volumes:
      - grafana-storage:/var/lib/grafana
volumes:
  grafana-storage: {}
```

## Key Components of the Configuration

#### Service: Grafana

###### **Image**: 

* <code>grafana/grafana</code> is the Docker image used for Grafana.

###### **Ports**:

* <code>3000:3000</code> maps port 3000 on the host to port 3000 in the container, where Grafana's web interface is accessible.

###### **Volumes**:

* <code>grafana-storage:/var/lib/grafana</code> provides persistent storage for Grafana's data.

###### **Restart Policy**: 

* <code>unless-stopped</code> ensures that the Grafana service restarts automatically unless explicitly stopped.

## Deploying Grafana

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> to start Grafana in detached mode.

3. Access Grafana by navigating to <code>http://<host-ip>:3000</code>.

## Configuring and Using Grafana

After deployment, configure Grafana through its web interface to connect to your data sources, create dashboards, and set up alerts.

