# Setting Up Prometheus with Docker Compose

## Introduction to Prometheus

Prometheus is an open-source monitoring and alerting toolkit, widely used for its powerful querying language, efficient storage, and ease of integration with various metrics sources.

## Docker Compose Configuration for Prometheus

This Docker Compose setup deploys Prometheus in a Docker container, along with a specified configuration file for custom monitoring settings.

#### Docker Compose File (docker-compose.yml)

```yaml
version: '3.8'
services:
  prometheus:
    image: prom/prometheus
    container_name: prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
    ports:
      - 9090:9090
    restart: unless-stopped
    volumes:
      - ./prometheus:/etc/prometheus
      - prom_data:/prometheus
volumes:
  prom_data:
```

#### Prometheus Configuration File (prometheus.yml)

```yaml
global:
  scrape_interval: 15s
  scrape_timeout: 10s
  evaluation_interval: 15s
alerting:
  alertmanagers:
    - static_configs:
      - targets: []
      scheme: http
      timeout: 10s
      api_version: v1
scrape_configs:
  - job_name: prometheus
    honor_timestamps: true
    scrape_interval: 15s
    scrape_timeout: 10s
    metrics_path: /metrics
    scheme: http
    static_configs:
      - targets:
        - localhost:9090
  - job_name: elzim # Change to whatever you like
    static_configs:
      - targets: ['192.168.68.109:9100'] #Change this to your server's IP
```

## Key Components of the Configuration

#### Service: Prometheus

###### Image: 

* <code>prom/prometheus</code> is the Docker image used for Prometheus.

###### Command: 

* <code>--config.file=/etc/prometheus/prometheus.yml</code> specifies the configuration file used by Prometheus.

###### Ports:

* <code>9090:9090</code> maps port 9090 on the host to port 9090 in the container, where Prometheus's web interface is accessible.

###### Volumes:

* <code>./prometheus:/etc/prometheus</code> mounts the local Prometheus configuration directory to the container.

* <code>prom_data:/prometheus</code> provides persistent storage for Prometheus data.

###### Restart Policy: 

* <code>unless-stopped</code> ensures that Prometheus restarts automatically unless explicitly stopped.

#### Prometheus Configuration

* **Global Settings**: Defines the global scrape interval, timeout, and evaluation interval.

* **Alerting**: Configuration for alert managers.

* **Scrape Configs**: Defines the jobs and targets for Prometheus to scrape metrics from.

## Deploying Prometheus

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file and the Prometheus configuration in a <code>prometheus.yml</code> file.

2. Run <code>docker compose up -d</code> to start Prometheus in detached mode.

3. Access Prometheus's web interface via <code>http://host-ip:9090</code>.

## Configuring and Using Prometheus

After deployment, you can modify the <code>prometheus.yml</code> file to add new targets and change scrape intervals as needed. Prometheus provides a versatile platform for monitoring your infrastructure.