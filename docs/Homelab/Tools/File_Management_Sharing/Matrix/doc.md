# Setting Up Synapse Matrix Server with Docker: A Complete Guide

## Introduction to Synapse Matrix Server

Synapse Matrix Server provides a robust platform for secure, decentralized communication. It supports instant messaging, VoIP, and file transfers, making it an excellent choice for individuals and organizations looking for a private communication solution.

## Deployment Steps for Synapse Matrix Server

This guide will walk you through deploying the Synapse Matrix Server using Docker, configuring essential settings, and enabling user registration.

#### Docker Compose Setup

###### Docker Compose File:

```yaml
version: '3.3'
services:
  synapse:
    container_name: synapse
    image: matrixdotorg/synapse:latest
    restart: always
    ports:
      - 8008:8008
    volumes:
      - ./data:/data
```

1. Prepare the Data Directory.

2. Create a <code>data</code> directory alongside your <code>docker-compose.yml</code>. This prevents Docker from setting it up as owned by <code>root</code>, which can complicate file permissions.

3. Generate Matrix Configuration

4. Run the following command to generate the Matrix configuration files. Replace <code>matrix.elzim.xyz</code> with your server name:

```commandline
docker run -it --rm -v ./data:/data -e SYNAPSE_SERVER_NAME=matrix.elzim.xyz -e SYNAPSE_REPORT_STATS=yes matrixdotorg/synapse:latest generate
```

5. Adjust Ownership of the Data Directory.

6. Files in the <code>data</code> directory may be owned by <code>root</code>. Change the ownership to UID 991 with the following command:

```commandline
sudo chown -R 991:991 data/
```

7. This ensures Synapse can access its configuration and data files.

8. Enable User Registration.

9. Edit the <code>homeserver.yaml</code> file in the <code>data</code> directory: Let's incorporate the provided <code>homeserver.yaml</code> configuration details into the documentation for setting up Synapse Matrix Server using Docker. This includes steps for enabling user registration and configuring reCAPTCHA.

After generating the Synapse configuration files and adjusting file ownership, the next crucial step is to configure your Synapse server to allow user registration and enhance security with reCAPTCHA.

## Editing homeserver.yaml

#### Sample File

```yaml
# Basic server information
server_name: "your.domain.com"  # The domain name of your Matrix server.
pid_file: /data/homeserver.pid  # Path to the PID file for the Synapse process.

# Networking
listeners:
  - port: 8008
    tls: false
    type: http
    x_forwarded: true  # Enables handling of X-Forwarded-For headers.
    resources:
      - names: [client, federation]
        compress: false

# Database settings
database:
  name: sqlite3
  args:
    database: /data/homeserver.db  # Path to the SQLite database file.

# Logging
log_config: "/data/your.domain.com.log.config"  # Path to the logging configuration file.

# Media storage
media_store_path: /data/media_store  # Where media files are stored on the disk.

# Registration and authentication
registration_shared_secret: "your_secret"  # A secret used to authorize registration requests.
enable_registration: true  # Allows users to register on your server.
enable_registration_captcha: true  # Enables CAPTCHA for registrations.

# reCAPTCHA settings
recaptcha_public_key: "your_public_key"
recaptcha_private_key: "your_private_key"
recaptcha_siteverify_api: "https://www.google.com/recaptcha/api/siteverify"

# Privacy
report_stats: true  # Whether to report anonymous statistics to the Matrix.org project.

# Security
macaroon_secret_key: "your_macaroon_secret"
form_secret: "your_form_secret"
signing_key_path: "/data/your.domain.com.signing.key"  # Path to the server's signing key.

# Federation
trusted_key_servers:
  - server_name: "matrix.org"  # Trusted server for key validation.
```

Locate the <code>homeserver.yaml</code> file within the <code>data</code> directory you've created and make the following adjustments:

#### Basic Server Information

* <code>server_name</code>: This should be the domain name of your Matrix server. Replace <code>"your.domain.com"</code> with your actual domain name.

* <code>pid_file</code>: Specifies the path to the PID file for the Synapse process. It's set to <code>/data/homeserver.pid</code> by default.

#### Networking

* The <code>listeners</code> configuration allows your server to handle HTTP connections on port <code>8008</code> and properly manage <code>X-Forwarded-For</code> headers if you're running Synapse behind a reverse proxy.

#### Database Settings

* Synapse uses SQLite by default for simplicity, indicated by the <code>"sqlite3"</code> <code>name</code>. The <code>database</code> argument points to the SQLite database file path.

#### Logging

* <code>log_config</code>: Path to the Synapse logging configuration file. Replace <code>"your.domain.com.log.config"</code> with the appropriate path, ensuring it matches your domain.

#### Media Storage

* <code>media_store_path</code>: Defines where media files uploaded to the server are stored on disk.

#### Registration and Authentication

* <code>enable_registration</code>: Set to <code>true</code> to allow users to register on your server without an invitation.

* <code>enable_registration_captcha</code>: Set to <code>true</code> and configure Google reCAPTCHA to prevent automated spam registrations.

#### reCAPTCHA Settings

* <code>recaptcha_public_key</code> and <code>recaptcha_private_key</code>: Obtain these from Google's reCAPTCHA admin console by creating a new site with reCAPTCHA v2 ("I'm not a robot" Checkbox). Include your server's domain in the list of authorized domains.

* <code>recaptcha_siteverify_api</code>: The API URL used to verify the reCAPTCHA response.

## Configuring Google reCAPTCHA

1. Go to Google reCAPTCHA admin console to create a new site.

2. Set the label and choose reCAPTCHA v2 with the "I'm not a robot" Checkbox.

3. Add your server's domain to the list of authorized domains.

4. Copy the site key and secret key into <code>homeserver.yaml</code> under <code>recaptcha_public_key</code> and <code>recaptcha_private_key</code>, respectively.

5. Ensure <code>enable_registration_captcha: true</code> is set in your <code>homeserver.yaml</code>.

By following these steps, you've configured your Synapse server to allow user registrations while protecting against spam with Google reCAPTCHA. Continue with the deployment by running <code>docker compose up -d</code>, and proceed to create a local admin account to start managing your Matrix server.

1. Creating a Local Admin Account.

2. Use the following command to create an admin account. Replace <code>admin</code> and <code>testing123@!</code> with your desired username and password:

```commandline
docker exec -it synapse register_new_matrix_user -u admin -p testing123@! -a -c /data/homeserver.yaml http://localhost:8008
```

3. Start Synapse Matrix Server.

4. With the configuration complete, start your server:

```commandline
docker compose up -d
```

5. Ensure everything is running smoothly by accessing the server locally.

#### Making Your Server Public

For those looking to make their Synapse Matrix Server accessible publicly, setting up a Cloudflare Tunnel is a secure and effective method. Refer to this video tutorial for a step-by-step guide on deploying Cloudflare Tunnel.

#### Connecting with a Matrix Client

Once your server is up and running, you can connect using any Matrix-compatible client, such as Element, by pointing it to your server's URL.

By following these detailed steps, you'll have a fully functional Synapse Matrix Server ready for secure communication across your devices and with others on the Matrix network.