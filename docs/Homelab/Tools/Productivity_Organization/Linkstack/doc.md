# Setting Up Linkstack with Docker Compose

## Introduction to Linkstack

Linkstack is a web application that provides a user-friendly platform for managing and organizing web links. It is designed for ease of use and convenience in storing a collection of links.

## Docker Compose Configuration for Linkstack

This Docker Compose setup deploys Linkstack in a Docker container, offering a dedicated environment for link management.

#### Docker Compose File (docker-compose.yml)

```yaml
version: '3.8'

services:
  linkstack:
    image: linkstackorg/linkstack
    container_name: linkstack
    hostname: linkstack
    environment:
      #HTTP_SERVER_NAME: "www.example.xyz"
      #HTTPS_SERVER_NAME: "www.example.xyz"
      SERVER_ADMIN: "[email protected]"
      TZ: "Pacific/Auckland"
      PHP_MEMORY_LIMIT: "512M"
      UPLOAD_MAX_FILESIZE: "8M"
    ports:
      - "8099:80"
      - "8443:443"
    restart: unless-stopped
    volumes:
      - "linkstack:/htdocs"
volumes:
  linkstack:
```

## Key Components of the Configuration

#### Service: Linkstack

###### **Image**: 

* <code>linkstackorg/linkstack</code> is the Docker image used for Linkstack.

###### **Environment Variables**:

* <code>SERVER_ADMIN</code>: Email address of the server administrator.

* <code>TZ</code>: Timezone set to "Pacific/Auckland".

* <code>PHP_MEMORY_LIMIT</code>: PHP memory limit set to "512M".

* <code>UPLOAD_MAX_FILESIZE</code>: Maximum file upload size set to "8M".

* <code>HTTP_SERVER_NAME</code> and <code>HTTPS_SERVER_NAME</code> are commented out and can be set as needed.

###### Ports:

* <code>8099:80</code> maps HTTP traffic from port 8099 on the host to port 80 in the container.

* <code>8443:443</code> maps HTTPS traffic from port 8443 on the host to port 443 in the container.

###### Volumes:

* <code>linkstack:/htdocs</code> provides persistent storage for Linkstack's data.

###### Restart Policy: 

* <code>unless-stopped</code> ensures that Linkstack restarts automatically unless explicitly stopped.

## Deploying Linkstack

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> to start Linkstack in detached mode.

3. Access Linkstack's web interface via <code>http://<host-ip>:8099</code>.

## Configuring and Using Linkstack

After deployment, configure Linkstack through its web interface to start organizing and managing your web links.