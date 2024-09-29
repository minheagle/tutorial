# Setting Up Filebrowser with Docker Compose

## Introduction to Filebrowser

Filebrowser is a self-hosted file managing interface that allows you to manage files and directories through a web interface. It's a simple and convenient way to access, upload, and manage your files remotely.

## Docker Compose Configuration for Filebrowser

This Docker Compose setup deploys Filebrowser in a Docker container, providing an easy-to-use web interface for file management.

#### Docker Compose File (docker-compose.yml)

```yaml
version: '3'
services:
  filebrowser:
    image: filebrowser/filebrowser:latest
    container_name: filebrowser
    volumes:
      - /home:/srv #Change to match your directory
      - /home/techdox/docker/filebrowser/filebrowser.db:/database/filebrowser.db #Change to match your directory
      - /home/techdox/docker/filebrowser/settings.json:/config/settings.json #Change to match your directory
    environment:
      - PUID=$(id -u)
      - PGID=$(id -g)
    ports:
      - 8095:80 #Change the port if needed
```

## Key Components of the Configuration

#### Service: Filebrowser

###### Image: 

* <code>filebrowser/filebrowser:s6</code> is the Docker image used for Filebrowser.

###### Volumes:

* <code>/home:/srv</code>: Maps a local directory to the server directory in the container.

* <code>/home/techdox/docker/filebrowser/filebrowser.db:/database/filebrowser.db</code>: Persistent storage for Filebrowser's database.

* <code>/home/techdox/docker/filebrowser/settings.json:/config/settings.json</code>: Stores configuration settings for Filebrowser.

###### Environment Variables:

* <code>PUID=$(id -u)</code> and <code>PGID=$(id -g)</code>: Sets the user and group ID for file permissions.

###### Ports:

* <code>8095:80</code>: Maps port 8095 on the host to port 80 in the container, where Filebrowser's web interface is accessible.

## Deploying Filebrowser

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Replace the volume paths with your actual directory paths.

3. Manually create the filebrowser.db and settings.json by running <code>touch filebrowser.db</code> <code>touch settings.json</code> in the compose directory, if you do not do this you will get permission errors.

4. Run <code>docker compose up -d</code> to start Filebrowser in detached mode.

5. Access Filebrowser by navigating to <code>http://<host-ip>:8095</code>.

6. Default login is <code>admin</code> <code>admin</code>

## Configuring and Using Filebrowser

After deployment, use the Filebrowser web interface to manage your files. You can upload, download, and organize files, as well as customize settings according to your needs.