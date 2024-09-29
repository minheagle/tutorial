# Setting Up Memos with Docker Compose

## Introduction to Memos

Memos is a self-hosted note-taking application that offers a convenient way to organize and store personal notes, memos, and other pieces of information.

## Docker Compose Configuration for Memos
This Docker Compose setup deploys Memos in a Docker container, providing an easy-to-manage environment for your note-taking needs.

#### Docker Compose File (docker-compose.yml)

```yaml
version: "3.0"
services:
  memos:
    image: neosmemo/memos:latest
    container_name: memos
    volumes:
      - ~/.memos/:/var/opt/memos
    ports:
      - 5230:5230
```

## Key Components of the Configuration

#### Service: Memos

###### Image: 

* <code>neosmemo/memos:latest</code> is the Docker image used for Memos.

###### Volumes:

* <code>~/.memos/:/var/opt/memos</code> maps a local directory (<code>~/.memos/</code>) to the container's data storage directory (<code>/var/opt/memos</code>). This is where Memos stores its data.

###### Ports:

* <code>5230:5230</code> maps port 5230 on the host to port 5230 in the container, where Memos's web interface is accessible.

###### Restart Policy

* Not specified in the Compose file, but the default is <code>no</code> which means the container does not automatically restart. It's recommended to set a restart policy like <code>unless-stopped</code>.

## Deploying Memos

1. Save the Docker Compose configuration in a <code>docker-compose.yml</code> file.

2. Run <code>docker compose up -d</code> to start Memos in detached mode.

3. Access Memos by navigating to <code>http://<host-ip>:5230</code>.

## Configuring and Using Memos

After deployment, you can start using Memos through its web interface for creating and managing your notes.