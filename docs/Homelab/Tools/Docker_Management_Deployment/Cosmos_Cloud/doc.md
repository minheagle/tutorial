# Deploying Cosmos Cloud Server with Docker

## Introduction to Cosmos Cloud

Cosmos Cloud is a sophisticated platform designed to manage Docker containers and services. It provides an intuitive interface for container orchestration, simplifying the deployment and management of Dockerized applications.

## Docker Run Command for Cosmos Cloud Server

The recommended method to deploy Cosmos Cloud Server is via a Docker run command. This approach is advised by Cosmos Cloud developers for optimal compatibility and performance.

#### Docker Run Command Breakdown

```commandline
docker run -d --network host --privileged --name cosmos-server -h cosmos-server --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /:/mnt/host -v /var/lib/cosmos:/config azukaar/cosmos-server:latest
```

!!! Warning
    For Windows and MacOS users: Please use the command below. This adjustment is necessary due to Docker's different handling of network interfaces and privileges on non-Linux platforms.

```commandline
docker run -d -p 80:80 -p 443:443 -p 4242:4242/udp --privileged --name cosmos-server -h cosmos-server --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /:/mnt/host -v ./config:/config azukaar/cosmos-server:latest
```

!!! Note
    To change the default ports: -e COSMOS_HTTP_PORT=8080 -e COSMOS_HTTPS_PORT=8443 Change these port values to your own

* <code>-d</code>: Run container in detached mode (in the background).

* <code>--network host</code>: Use the host's networking stack. This is crucial for Cosmos Cloud to properly manage and communicate with other containers.

* <code>--privileged</code>: Gives the container full access to the host. This is necessary for Cosmos Cloud to manage Docker containers and host resources effectively.

* <code>--name cosmos-server</code>: Assigns the container a name for easy reference.

* <code>-h cosmos-server</code>: Sets the hostname of the container to cosmos-server.

* <code>--restart=always</code>: Ensures the container automatically restarts if it stops unexpectedly (e.g., due to a system reboot or crash).

* <code>-v /var/run/docker.sock:/var/run/docker.sock</code>: Mounts the Docker socket file from the host inside the container. This allows Cosmos Cloud to interact with the Docker daemon, managing containers and services.

* <code>-v /:/mnt/host</code>: Mounts the root filesystem of the host to <code>/mnt/host</code> inside the container. This gives Cosmos Cloud access to the host's file system for management and monitoring purposes.

* <code>-v /var/lib/cosmos:/config</code>: Persists Cosmos Cloud's configuration data in <code>/var/lib/cosmos</code> on the host.

* <code>azukaar/cosmos-server:latest</code>: Specifies the Docker image and tag to use for the container.

## Important Note on Deployment Method

Cosmos Cloud explicitly states: "**DO NOT USE DOCKER-COMPOSE, UNRAID TEMPLATES, CASAOS, OR PORTAINER STACKS TO INSTALL COSMOS. IT WILL NOT WORK PROPERLY. JUST RUN THE DOCKER RUN COMMAND!**" This directive is due to Cosmos Cloud's specific networking and host resource management requirements that cannot be properly configured or fully supported through these tools.

Using Docker Compose or similar tools might restrict certain necessary privileges or configurations that Cosmos Cloud needs for its operation, such as <code>--network host</code> or <code>--privileged</code> modes. Such limitations could lead to incomplete functionality or prevent Cosmos Cloud from operating as intended.

## Deployment Instructions

1. **Prepare Your System**: Ensure Docker is installed and running on your host system.

2. **Run the Docker Command**: Execute the provided Docker run command in your terminal. This command pulls the latest Cosmos Cloud Server image and starts a new container with the appropriate configurations.

3. **Access Cosmos Cloud**: After deployment, access Cosmos Cloud through its web interface or according to its documentation to start managing your Docker containers and services.

By following these instructions and using the Docker run command as recommended by Cosmos Cloud, you ensure a smooth and functional deployment of Cosmos Cloud Server, ready to orchestrate your containerized applications effectively.