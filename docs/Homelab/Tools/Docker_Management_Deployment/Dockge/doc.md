# Setting Up Dockge with Docker

## Introduction to Dockge

Dockge is a self-hosted, reactive Docker stack manager, offering an easy-to-use interface for managing Docker containers and compose stacks. It's created by the same developer as Uptime-Kuma.

## Recommended Docker Compose Setup for Dockge

Instead of directly using the setup from the project page, the following steps are recommended for a smoother setup experience:

1. **Create Dockge Directory**: Navigate to the directory where you keep your Docker containers. For example, if you store them in <code>~/Docker</code>, the commands would be:

    ```commandline
    cd ~/Docker
    ```
    
    ```commandline
    mkdir dockge
    ```
    
    ```commandline
    cd dockge
    ```

2. **Link Your Containers Directory**: Check if <code>/opt/stacks</code> exists, and if not, create and link it to your containers' location:

    Check if it exists
    ```commandline
    ls /opt/stacks
    ```
    
    ```commandline
    sudo mkdir -p /opt/stacks
    ```
    
    ```
    sudo ln -s path-to-your-containers /opt/stacks
    ```
    
    ```
    # Example: sudo ln -s /Users/<username>/Docker /opt/stacks
    # Do not use ~/ in the above command
    ```
    
    Replace <code>path-to-your-containers</code> with the actual path to your Docker containers.

3. **Download and Start Dockge**: Download the <code>compose.yaml</code> file and start the Dockge service:

    ```commandline
    curl https://raw.githubusercontent.com/louislam/dockge/master/compose.yaml --output compose.yaml
    ```
   
## Docker Compose File (docker-compose.yml)

Here's an example <code>docker-compose.yml</code> file for Dockge:

```yaml
version: "3.8"
services:
  dockge:
    image: louislam/dockge:latest
    restart: unless-stopped
    ports:
      - 5005:5001
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./data:/app/data
      - /opt/stacks:/opt/stacks
    environment:
      - DOCKGE_STACKS_DIR=/opt/stacks
```

## Key Components of the Configuration

#### Service: Dockge

###### **Image**: 

* <code>louislam/dockge:latest</code> is the Docker image used for Dockge.

###### **Ports**:

* <code>5005:5001</code> maps port 5005 on the host to port 5001 in the container, where Dockge's web interface is accessible.

###### **Volumes**:

* <code>/var/run/docker.sock:/var/run/docker.sock</code> allows Dockge to interact with the Docker daemon.

* <code>./data:/app/data</code> provides persistent storage for Dockge's data.

* <code>/opt/stacks:/opt/stacks</code> maps a local directory for Docker stacks.

###### Environment Variables:

* <code>DOCKGE_STACKS_DIR=/opt/stacks</code> sets the directory path for Docker stacks within Dockge.

## Deploying Dockge

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> to start Dockge in detached mode.

3. Access Dockge's web interface by navigating to <code>http://host-ip:5005</code>.

## Configuring and Using Dockge

After deployment, use the Dockge web interface to manage your Docker containers, images, and stacks. The interface provides tools for monitoring, starting, stopping, and removing Docker components.