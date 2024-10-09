# Installation

## Install Docker Compose

```commandline
mkdir jenkins
```

```commandline
cd jenkins
```

```commandline
touch docker-compose.yml
```

```yaml
services:
  jenkins:
    image: jenkins/jenkins:lts
    privileged: true
    user: root
    ports:
      - 8080:8080
      - 50000:50000
    container_name: jenkins
    volumes:
      - ./jenkins_home:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
      - /usr/local/bin/docker:/usr/local/bin/docker
    restart: unless-stopped
```

```commandline
docker compose up -d
```

```commandline
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```