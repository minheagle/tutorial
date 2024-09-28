# Setting Up Chibisafe with Docker Compose

## Introduction to Chibisafe

Chibisafe is a file uploader and manager that's easy to use, allowing for the quick and secure sharing of files. It's a self-hosted solution for those who need control over their file-sharing environment.

## Docker Compose Configuration for Chibisafe

This Docker Compose setup deploys Chibisafe in a Docker container, streamlining the process of managing and sharing files securely.

#### Docker Compose File (docker-compose.yml)

```
version: "3.7"

services:
  chibisafe:
    image: chibisafe/chibisafe:latest
    container_name: chibisafe
    volumes:
      - ./database:/home/node/chibisafe/database:rw
      - ./uploads:/home/node/chibisafe/uploads:rw
      - ./logs:/home/node/chibisafe/logs:rw
    ports:
      - 24424:8000
    restart: always
```

#### Key Components of the Configuration

###### Service: Chibisafe

* **Image**: <code>chibisafe/chibisafe:latest</code> is the Docker image used for Chibisafe.
* **Volumes**:
    * <code>./database:/home/node/chibisafe/database:rw</code> stores Chibisafe's database files.
    * <code>./uploads:/home/node/chibisafe/uploads:rw</code> stores the uploaded files.
    * <code>./logs:/home/node/chibisafe/logs:rw</code> stores logs. Each of these folders needs to be created manually before starting the container to avoid permission issues.
* Ports:
    * <code>24424:8000</code> maps port 24424 on the host to port 8000 in the container, where Chibisafe's web interface is accessible.
* **Restart Policy**: <code>always</code> ensures that Chibisafe restarts automatically after a crash or reboot.

#### Preparing for Deployment

1. **Manual Directory Creation**: Before running <code>docker compose up -d</code>, manually create the <code>database</code>, <code>uploads</code>, and <code>logs</code> directories within the same directory as your <code>docker-compose.yml</code> file. This step is important to prevent permission issues that can arise when these directories are automatically created by Docker, possibly under the root user.

2. **Defining the App URL**: If you plan to publish Chibisafe publicly, ensure to define the application URL within Chibisafe's configuration. This step is crucial for proper functionality and access.

#### Deploying Chibisafe

1. After manually creating the necessary directories, save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> to start Chibisafe in detached mode.

3. Access Chibisafe by navigating to <code>http://<host-ip>:24424</code>.

#### Configuring and Using Chibisafe

Post-deployment, dive into Chibisafe's settings to customize your file-sharing environment. Remember, the initial setup like directory creation and app URL definition plays a significant role in the smooth operation of Chibisafe.

