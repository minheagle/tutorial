# Duplicati - Docker Setup

## Setting Up Duplicati with Docker Compose

#### Introduction to Duplicati: 

Duplicati is a free and open-source backup software that allows you to securely store backups online in various standard protocols and services. It's known for its versatility and ease of use, providing features like encryption, compression, and scheduling.

#### Docker Compose Configuration for Duplicati:

The following Docker Compose configuration will help you set up Duplicati in a Docker environment. This ensures a consistent and isolated setup for your backup needs.

#### Docker Compose File (docker-compose.yml):

```
version: "2.1"
services:
  duplicati:
    image: lscr.io/linuxserver/duplicati:latest
    container_name: duplicati
    environment:
      - PUID=0
      - PGID=0
      - TZ=Etc/UTC
      - CLI_ARGS= #optional
    volumes:
      - ./config:/config
      - ./backups:/backups
      - /:/source
    ports:
      - 8200:8200
    restart: unless-stopped
```

#### Key Components of the Configuration:

###### Image: 

Utilizes the <code>lscr.io/linuxserver/duplicati:latest</code> image, ensuring you have the latest version of Duplicati.

###### Container Name:

Sets the container's name to <code>duplicati</code> for easy identification and management.

###### Environment Variables:

* <code>PUID</code> and <code>PGID</code>: Sets user/group ID (here both are set to <code>0</code> for root).

* <code>TZ</code>: Timezone configuration, set to <code>Etc/UTC</code>.

* <code>CLI_ARGS</code>: Optional field for additional command-line arguments.

###### Volumes:

* <code>./config:/config</code>: Mounts the local <code>config</code> directory to store Duplicati's configuration files.

* <code>./backups:/backups</code>: Designated local directory for storing backups.

* <code>/:/source</code>: Mounts the root directory of the host to the container, allowing access to all files for backup.

###### Ports: 

* Maps port <code>8200</code> of the host to port <code>8200</code> of the container, facilitating access to the Duplicati web interface.

###### Restart Policy: 

The <code>unless-stopped</code> policy ensures that the container restarts automatically unless explicitly stopped.

#### Deploying Duplicati:

1. Save the above Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> in the directory containing this file to start Duplicati in detached mode.

3. Once running, access the Duplicati web interface via <code>http://<host-ip>:8200</code>.

#### Configuring and Using Duplicati: 

After deployment, you can configure backup jobs, schedules, and destinations through the Duplicati web interface. Ensure to properly set up encryption and choose a reliable backup destination to secure your data.