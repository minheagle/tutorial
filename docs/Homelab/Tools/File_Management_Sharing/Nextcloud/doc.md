# Setting Up Nextcloud with Docker Compose

## Introduction to Nextcloud

Nextcloud is an open-source, self-hosted file share and collaboration platform. It provides a secure and private alternative to cloud-based storage services.

## Docker Compose Configuration for Nextcloud

This setup includes Nextcloud and a MariaDB database, ensuring an isolated and manageable environment.

#### Docker Compose File (docker-compose.yml)

```yaml
version: '2'

volumes:
  nextcloud:
  db:

services:
  db:
    image: mariadb:10.6
    restart: always
    command: --transaction-isolation=READ-COMMITTED --log-bin=binlog --binlog-format=ROW
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=<ENTER PASSWORD HERE>
      - MYSQL_PASSWORD=<ENTER PASSWORD HERE>
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    restart: always
    ports:
      - 8080:80
    links:
      - db
    volumes:
      - nextcloud:/var/www/html
    environment:
      - MYSQL_PASSWORD=<ENTER PASSWORD HERE>
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
```

## Key Components of the Configuration

#### Volumes

* **nextcloud**: Stores Nextcloud's data.
* **db**: Stores the MariaDB database files.
#### Services

###### **db**

* **Image**: <code>mariadb:10.6</code>
* **Restart**: Always ensures the container restarts after a crash or reboot.
* **Command**: Configures MariaDB for optimal use with Nextcloud.
* **Volumes**: Maps <code>db</code> volume to MariaDB data directory.
* **Environment Variables**: Set the MySQL root and Nextcloud user passwords, database, and user.

###### **app**

* **Image**: <code>nextcloud</code>
* **Restart**: Always ensures the container restarts after a crash or reboot.
* **Ports**: Maps port 8080 of the host to port 80 of the container.
* **Links**: Connects to the <code>db</code> service.
* **Volumes**: Maps <code>nextcloud</code> volume to Nextcloud's HTML directory.
* **Environment Variables**: Set the database details for Nextcloud to connect to MariaDB.

## Deploying Nextcloud

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Replace <code><ENTER PASSWORD HERE></code> with your chosen passwords.

3. Run <code>docker compose up -d</code> to start Nextcloud in detached mode.

4. Access Nextcloud via <code>http://<host-ip>:8080</code>.

## Configuring and Using Nextcloud

After deployment, configure your Nextcloud instance through its web interface. This includes admin account setup, storage management, and app configurations.

