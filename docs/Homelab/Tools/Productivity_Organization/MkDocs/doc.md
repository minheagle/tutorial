# Setting Up MkDocs with Docker Compose

## Introduction to MkDocs

MkDocs is a static site generator that's geared towards project documentation. With the Material theme, it provides a sleek, responsive, and user-friendly interface for your documentation projects.

## Docker Compose Configuration for MkDocs

This Docker Compose setup deploys MkDocs with the Material theme in a Docker container, allowing you to easily manage and preview your project documentation.

#### Docker Compose File (docker-compose.yml)

```yaml
version: '3'
services:
  mkdocs:
    image: squidfunk/mkdocs-material
    ports:
      - "8005:8000"
    volumes:
      - ./:/docs
    stdin_open: true
    tty: true
```

## Key Components of the Configuration

#### Service: MkDocs

###### Image: 

* <code>squidfunk/mkdocs-material</code> is the Docker image used for MkDocs with the Material theme.

###### Ports:

* <code>8005:8000</code> maps port 8005 on the host to port 8000 in the container, where MkDocs's web interface is accessible.

###### Volumes:

* <code>./:/docs</code>: Maps the current directory (project documentation) to the <code>/docs</code> directory in the container.

###### Interactive Mode:

* <code>stdin_open: true</code> and <code>tty: true</code> allow interactive processes, which is useful for live reloading during documentation development.

## Deploying MkDocs

To deploy MkDocs with Docker Compose, follow these steps:

1. Create a New Directory.

2. Create a new directory on your host system for your MkDocs container. You can name it <code>mkdocs</code> or any other name of your choice.

3. Docker Compose File.

4. Inside this new directory, create a <code>docker-compose.yml</code> file.

5. Save the following Docker Compose configuration into this file:

    ```yaml
    version: '3'
    services:
      mkdocs:
        image: squidfunk/mkdocs-material
        ports:
          - "8005:8000"
        volumes:
          - ./:/docs
        stdin_open: true
        tty: true
    ```

6. Create Documentation Directory.

7. Within the <code>mkdocs</code> directory, create another directory called <code>docs</code>. This will hold all your documentation files.

8. Create MkDocs Configuration File.

9. In the root of your <code>mkdocs</code> directory, create a file named <code>mkdocs.yml</code>.

10. Add the following base structure to the <code>mkdocs.yml</code> file:

    ```yaml
    site_name: Techdox Doc
    
    nav:
      - Home: index.md
      - About: about.md
    
    theme:
      name: 'material'
    ```
    
    * Feel free to customize the <code>site_name</code>, navigation (<code>nav</code>), and other configurations as needed.

11. Start the MkDocs Container.

12. Run <code>docker compose up -d</code> from within the <code>mkdocs</code> directory. This command starts the MkDocs container in detached mode.

13. Access MkDocs.

14. Once the container is running, access your MkDocs site by navigating to <code>http://<host-ip>:8005</code>.

15. You should see your MkDocs site with the Material theme, ready for further customization and document addition.

By following these steps, you will have a fully functional MkDocs site running in a Docker container, which you can access and edit as needed.

## Example MkDocs Configuration (mkdocs.yml)

This example demonstrates how to configure an MkDocs site with subpages, plugins, and additional features.

```yaml
site_name: Techdox Docs
nav:
  - Home: index.md
  - About: about.md
  - Docker Containers:
      - Overview: docker-containers.md
      - Adguard: adguard.md
      # Additional Docker container pages...
  - Networking:
      - Overview: networking-overview.md
      - GlusterFS: glusterfs.md
  # Additional sections...

theme:
  name: material
  logo: path/to/logo.png

markdown_extensions:
  - abbr
  - admonition
  - attr_list
  # Additional Markdown extensions...
  - pymdownx.arithmatex:
      generic: true
  - pymdownx.emoji:
      emoji_index: !!python/name:material.extensions.emoji.twemoji
      emoji_generator: !!python/name:material.extensions.emoji.to_svg
  - pymdownx.superfences
  # More pymdownx extensions...
```