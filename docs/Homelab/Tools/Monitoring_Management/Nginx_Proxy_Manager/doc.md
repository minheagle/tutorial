# Setting Up Nginx Proxy Manager with Docker Compose

## Introduction to Nginx Proxy Manager

Nginx Proxy Manager (NPM) simplifies the process of managing Nginx proxy configurations for web services. It provides an easy-to-use dashboard for setting up SSL, redirecting HTTP traffic to HTTPS, proxying websockets, and more.

## Docker Compose Configuration for Nginx Proxy Manager

This Docker Compose setup deploys Nginx Proxy Manager alongside a MariaDB database, ensuring a seamless and integrated environment for managing your proxies.

#### Docker Compose File (docker-compose.yml)

```yaml
version: '3.8'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'    # Public HTTP Port
      - '443:443'  # Public HTTPS Port
      - '81:81'    # Admin Web Port
    environment:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "npm"
      DB_MYSQL_PASSWORD: "npm"
      DB_MYSQL_NAME: "npm"
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
    depends_on:
      - db

  db:
    image: 'jc21/mariadb-aria:latest'
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: 'npm'
      MYSQL_DATABASE: 'npm'
      MYSQL_USER: 'npm'
      MYSQL_PASSWORD: 'npm'
    volumes:
      - ./mysql:/var/lib/mysql
```

## Key Components of the Configuration

#### Services:

###### **app (Nginx Proxy Manager):**

* **Ports**: Exposes the standard HTTP and HTTPS ports for proxy traffic, and a separate port for accessing the admin dashboard.

* **Environment**: Configures the database connection to the <code>db</code> service using environment variables.

* **Volumes**: Persists NPM data and LetsEncrypt certificates for SSL management.

###### **db (MariaDB):**

* **Environment**: Sets the database credentials and enables automatic database upgrades.

* **Volumes**: Stores the MariaDB data persistently.

#### Configuration Details:

* **Database Connection**: The <code>app</code> service is configured to connect to the <code>db</code> service for its database needs. The environment variables specify the host, port, username, password, and database name.

* **Volumes**:

    * <code>./data</code> and <code>./letsencrypt</code>: These directories on the host are mounted to the NPM container to store application data and SSL certificates, ensuring they persist across container restarts and deployments.
    * <code>./mysql</code>: This directory is mounted to the MariaDB container, preserving the database across restarts.

## Deployment Instructions

1. Prepare Environment.

2. Ensure the directories for the volumes exist on your host system. If not, create them to avoid permission issues.

3. Start Services.

4. Run <code>docker compose up -d</code> to start the Nginx Proxy Manager and the database.

5. Access Admin Dashboard.

6. Access the NPM admin dashboard through <code>http://<host-ip>:81</code> and proceed with the initial setup, including setting up your first admin user account.

#### Account:

* Email:

```
admin@example.com
```
   
* Password:
   
```
changeme
```
