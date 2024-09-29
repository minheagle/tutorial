# Deploying Wallos with Docker Compose

## Introduction to Wallos

Wallos is an open-source, self-hostable web application designed to simplify tracking your subscriptions and expenses. It provides an easy-to-use platform to manage your finances, replacing the need for complicated spreadsheets or expensive software. This guide details how to deploy Wallos using Docker Compose, with notes on configuring volumes to prevent permissions errors.

## Docker Compose Configuration for Wallos

Below is the Docker Compose file used to deploy Wallos, with explanations of the components involved.

#### Docker Compose File (docker-compose.yml)

```yaml
services:
  wallos:
    container_name: wallos                          # Names the container for easier management.
    image: bellamy/wallos:latest                    # Specifies the Wallos Docker image.
    ports:
      - "8282:80/tcp"                               # Exposes Wallos on port 8282.
    environment:
      TZ: 'America/Toronto'                         # Sets the timezone for the container.
    volumes:
      - './db:/var/www/html/db'                     # Stores Wallos' database for persistent data.
      - './logos:/var/www/html/images/uploads/logos' # Stores logos uploaded to the app.
    restart: unless-stopped                         # Ensures the container restarts automatically unless manually stopped.
```

#### Explanation of Key Components

###### Image: 

* Specifies the <code>bellamy/wallos:latest</code> Docker image, which contains the Wallos application.

###### Ports: 

* Maps port <code>8282</code> on the host to port <code>80</code> in the container, making Wallos accessible via <code>http://<your-server-ip>:8282</code>.

###### Environment:

* <code>TZ</code>: Sets the timezone for the container. In this example, it is set to <code>America/Toronto</code>, but you can adjust it to your local timezone.

###### Volumes:

* <code>./db:/var/www/html/db</code>: This volume ensures that the Wallos database is stored persistently on your host machine.

* <code>./logos:/var/www/html/images/uploads/logos</code>: This volume stores the logos uploaded to Wallos, ensuring they persist between container restarts.

    !!! Note
        You need to manually create the <code>db</code> and <code>logos</code> directories on your host system before running the container. Failing to do so may result in permissions errors or the container not starting properly.

#### Creating Required Directories

To avoid permission issues, make sure you create the required directories (<code>db</code> and <code>logos</code>) with proper permissions on your host machine:

```commandline
mkdir -p ./db ./logos
```

Ensure that Docker has access to these directories and that they are writeable by the container.

## Deployment

To deploy Wallos, navigate to the directory where your <code>docker-compose.yml</code> file is located and run:

```commandline
docker compose up -d
```

This command will start the Wallos service in detached mode, allowing it to run in the background.

## Accessing Wallos

Once deployed, you can access Wallos by navigating to:

```
http://<your-server-ip>:8282
```

From here, you can start managing your subscriptions and expenses with ease.

## Conclusion

Wallos provides a simple, self-hosted solution for tracking your subscriptions and managing your finances. By following this guide, you can deploy Wallos using Docker Compose and ensure that your data is stored persistently with proper volume management.